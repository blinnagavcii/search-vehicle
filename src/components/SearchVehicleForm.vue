<template>
    <div class="container">
        <form @submit.prevent="onSubmit" class="vehicle">
            <div class="vehicle__data">
                <select name="manufacturers" class="vehicle__select vehicle__manufacturers" v-model="selectedManufacturer">
                    <option v-for="(manufacturer, index) in manufacturers" :key="index" :value="manufacturer.name">
                        {{ manufacturer.name }}
                    </option>
                </select>

                <select name="models" class="vehicle__select vehicle__models" v-model="selectedModel" :disabled="isModelDisabled">
                    <option v-for="(model, index) in models" :key="index" :value="model.name">
                        {{ model.name }}
                    </option>
                </select>

                <select name="type" class="vehicle__select vehicle__type" v-model="selectedType" :disabled="isTypeDisabled">
                    <option v-for="(type, index) in types" :key="index" :value="type.name">
                        {{ type.name }}
                    </option>
                </select>
            </div>
            <div class="vehicle__submit">
                <button type="submit" :disabled="isSubmitDisabled">Submit</button>
            </div>
        </form>
    </div>
</template>

<script>
import Manufacturers from '@/json/manufacturers.json';
import Models from '@/json/models.json';
import Types from '@/json/types.json';

export default {
  name: 'SearchVehicleForm',
  data() {
      return {
        manufacturers: Manufacturers,
        models: Models,
        types: Types,
        selectedManufacturer: '',
        selectedModel: '',
        selectedType: '',
      };
  },
  computed: {
    isModelDisabled() {
        return !this.selectedManufacturer;
    },

    isTypeDisabled() {
        return !this.selectedModel;
    },

    isSubmitDisabled() {
        return this.selectedManufacturer === '' || this.selectedModel === '' || this.selectedType == '';
    }
  },
  methods: {
      onSubmit() {
          this.$emit('show-selected-vehicle', [this.selectedManufacturer, this.selectedModel, this.selectedType]);
      }
  },
}
</script>

<style lang="scss">
.container {
    display: flex;
    justify-content: center;
    align-content: center;
}

.vehicle {
    padding: 10px; 

    &__data {
        display: flex;
        justify-content: center;
        align-items: center;

        @media only screen and (max-width: 600px) {
            flex-direction: column;
        }
    }

    &__select {
        margin: 5px 5px;
        padding: 10px;
        border-radius: 5px;

        &:first-child {
            margin-left: 0;
        }

        &:last-child {
            margin-right: 0;
        }

        @media only screen and (max-width: 600px) {
            width: 100%;
            margin: 5px auto;
        }
    }

    &__submit button{
        width: 100%;
        margin: 7px 0px;
        background-color: #E1E1D2; /* Green */
        border: none;
        color: #000;
        padding: 15px 32px;
        text-align: center;
        text-decoration: none;
        border-radius: 5px;
        cursor: pointer;
        font-weight: bold;

        &:hover {
            background-color: #c0c0ab;
        }

        &:disabled {
            background-color: rgb(219, 219, 219);
            color: rgb(163, 163, 163);
            cursor: default;
        }
    }
}
</style>
