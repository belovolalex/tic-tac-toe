<template>
  <section class="cells">
    <Cell
      v-for="num in cellsCount"
      :key="num"
      @click.native="onClick(num)"
      :style="isSelected(num) ? { cursor: 'default' } : ''"
    >
      <span v-if="isSelected(num)">
        {{ getFigure(num) }}
      </span>
    </Cell>
    <Popup
      modal-name="result"
      @startNewGame="startNewGame"
    />
  </section>
</template>

<script>
  import Cell from './Cell'
  import Popup from './Popup'
  import { winningCombos } from '@/utils'

  export default {
    name: 'CellsComponent',
    components: { Cell, Popup },
    data() {
      return {
        countOfCellsInRow: 3,
        crossesMove: false,
        selectedCrosses: [],
        selectedZeros: []

      }
    },
    computed: {
      cellsCount() {
        return Math.pow(this.countOfCellsInRow, 2)
      },
      numberOfFilledCells() {
        return [...this.selectedCrosses, ...this.selectedZeros].length
      }
    },
    watch: {
      numberOfFilledCells(value) {
        if (value === this.cellsCount) {
          this.$modal.show('result', { result:  'Draw, try again'})
        }
      }
    },
    methods: {
      isInSelectedCrosses(num) {
        return this.selectedCrosses.includes(num)
      },
      isInSelectedZeros(num) {
        return this.selectedZeros.includes(num)
      },
      getFigure(num) {
        const CROSS = 'x'
        const ZERO = 'o'

        if (this.isInSelectedCrosses(num)) {
          return CROSS
        } else if(this.isInSelectedZeros(num)) {
          return ZERO
        }
      },
      onClick(num) {
        if(!this.isSelected(num)) {
          this.crossesMove = !this.crossesMove
          if(this.crossesMove) {
            this.selectedCrosses.push(num)
            this.checkWinner(this.selectedCrosses)
          } else {
            this.selectedZeros.push(num)
            this.checkWinner(this.selectedZeros)
          }
        }
      },
      checkWinner(selectedValues) {
        if(selectedValues.length >= this.countOfCellsInRow) {
          const result = winningCombos.some(combo => {
            return combo.every(value => selectedValues.indexOf(value) !== -1)
          })
          if(result) {
            const getWinnerName = () => this.crossesMove ? 'CROSSES': 'ZEROS'
            this.$modal.show('result', { result: `Congratulations! the winner is ${ getWinnerName() }` })
          }
        }
      },
      isSelected(num) {
        return this.isInSelectedCrosses(num) || this.isInSelectedZeros(num)
      },
      startNewGame() {
        this.crossesMove = false
        this.selectedCrosses = []
        this.selectedZeros = []
        this.$modal.hide('result')
      }
    }
  }
</script>

<style scoped>
  .cells {
    display: flex;
    flex-wrap: wrap;
    width: 300px;
    margin: auto;
  }
</style>
