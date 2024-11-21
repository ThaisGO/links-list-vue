<template>
    <base-dialog v-if="inputValid" title="Invalid Input">
        <!-- Usado porque dentro desse componente temos os slots, portanto precisamos injetar os códigos html nele -->
        <template v-slot:default>
            <p>Make sure the inputs are not empty.</p>
        </template>
            <!-- Poderíamos usar também essa nomenclatura no slot  -->
        <!-- <template #default></template>  -->

        <template #actions>
            <base-button @click="confirmError">Ok</base-button>
        </template>
    </base-dialog>

    <base-card>
        <form @submit.prevent="submitData">
            <div class="form-control">
                <label for="title">Title</label>
                <input type="text" name="title" id="title" ref="titleInput">
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea name="description" id="description" rows="3" ref="descInput"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input type="url" name="link" id="link" ref="linkInput">
            </div>
            <div>
                <base-button type="submit">Add Resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
    export default {
        inject: ['addResource'],
        data() {
            return {
                inputValid: false,
            }
        },
        methods: {
            submitData() {
                const enteredTitle = this.$refs.titleInput.value
                const enteredDescription = this.$refs.descInput.value
                const enteredUrl = this.$refs.linkInput.value

                if(enteredTitle.trim() === '' || enteredDescription.trim() === '' ||  enteredUrl.trim() === '') {
                    this.inputValid = true
                    return;
                }

                // Injetado do componente "TheResource"
                this.addResource(enteredTitle, enteredDescription, enteredUrl)
            },
            confirmError() {
                this.inputValid = false;
            }
        }
    }
</script>

<style scoped>
    label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>