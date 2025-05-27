<!-- src/App.vue -->
<template>
  <div class="bg-gray-100 min-h-screen flex items-center justify-center">
    <div class="bg-white p-8 rounded-lg shadow-md w-full max-w-2xl">
      <h1 class="text-2xl font-bold mb-6 text-center">Alignment Program Selection</h1>
      <form @submit.prevent="submitForm" class="space-y-4">
        <div>
          <label class="block mb-2 text-lg font-semibold">Sequence Input:</label>
          <textarea
            v-model="sequence"
            rows="10"
            class="w-full px-4 py-3 text-base border-2 border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent resize-y min-h-[250px]"
            placeholder="Paste or type your sequence here..."
            required
          ></textarea>
        </div>

        <div>
          <label class="block mb-2 text-lg font-semibold">Or Upload Sequence File:</label>
          <input
            type="file"
            @change="handleFileUpload"
            accept=".txt,.fasta,.seq,.gb"
            class="w-full px-4 py-3 border-2 border-gray-300 rounded-lg file:mr-4 file:rounded-md file:border-0 file:bg-blue-50 file:px-4 file:py-2 file:text-blue-700 hover:file:bg-blue-100 file:font-semibold"
          />
        </div>

        <div>
          <p class="mb-3 text-lg font-semibold">Select Alignment Programs:</p>
          <div class="space-y-3">
            <label
              v-for="[label, value] in Object.entries(options)"
              :key="value"
              class="flex items-center bg-gray-50 p-3 rounded-lg border border-gray-200 hover:bg-blue-50 transition duration-200"
            >
             <input
                type="checkbox"
                :value="value"
                v-model="selectedPrograms"
                class="w-5 h-5 text-blue-600 focus:ring-blue-500 border-gray-300 rounded mr-3"
              />
            <span class="text-base font-medium">{{ label }}</span>
         </label>

          </div>
        </div>

        <div>
          <label class="block mb-1 font-medium">Email Address:</label>
          <input
            type="email"
            v-model="email"
            class="w-full px-3 py-2 border rounded-md"
            required
          />
        </div>

        <button
          type="submit"
          class="w-full bg-blue-500 text-white py-2 rounded-md hover:bg-blue-600 transition duration-300"
        >
          Submit
        </button>

        <p v-if="error" class="text-red-500 mt-4">{{ error }}</p>
        <p v-if="response" class="text-green-600 mt-4">✅ Evaluation complete. Check your results!</p>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sequence: '',
      email: '',
      selectedPrograms: [],
      options: {
            'Muscle': 'muscle',
            'MAFFT': 'mafft',
            'DIALIGN': 'dalign',
            'T-Coffee': 't_coffee'
          },
      error: '',
      response: null,
    };
  },
  methods: {
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = (e) => {
        this.sequence = e.target.result;
      };
      reader.readAsText(file);
    },
    async submitForm() {
      this.error = '';
      this.response = null;

      if (!this.sequence || this.selectedPrograms.length === 0 || !this.email) {
        this.error = 'All fields are required and at least one program must be selected.';
        return;
      }

      try {
        const res = await fetch('http://localhost:8000/evaluate', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            sequence: this.sequence,
            email: this.email,
            programs: this.selectedPrograms,
          }),
        });

        if (!res.ok) throw new Error('Evaluation failed');

        this.response = await res.json();
      } catch (err) {
        this.error = err.message || 'Submission failed';
      }
    },
  },
};
</script>

<style scoped>
/*textarea:invalid,
input:invalid {
  border-color: red;
}*/
</style>
