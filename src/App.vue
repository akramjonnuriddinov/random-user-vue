<template>
  <div class="flex relative justify-center pt-10">
    <p class="absolute top-5 bg-white text-black rounded-2xl py-1 px-5">{{ gender }}</p>
    <div class="border-4 w-[150px] mb-4 rounded-full border-red-400">
      <img class="rounded-full" :src="profile" alt="" width="150" height="150">
    </div>
  </div>
  <div class="flex flex-col items-center">
    <h1 class="font-bold text-2xl mb-2 text-center">Salom, mening ismim <span>{{ name }}</span></h1>
    <p class="font-medium">{{ email }}</p>
    <p class="font-medium my-2">{{ phone }}</p>
    <button class="bg-black text-white px-4 py-3 rounded hover:opacity-90 ease-in">Tasodifiy inson</button>
  </div>
</template>

<script>
export default { 

   
  
  name: 'App',
  data() {
    return {
      KEY: `https://randomuser.me/api/`,
      name: '',
      email: '',
      phone: '',
      profile: '',
      gender: ''
    }
  },
  mounted() {
    this.setData();
  },
  methods: {
    async getData() {
      const res = await fetch(this.KEY);
      return res.json();
    },
    setData() {
      this.getData().then((e) => this.email = e.results[0].email)
      this.getData().then((e) => this.name = `${e.results[0].name.first} ${e.results[0].name.last}`)
      this.getData().then((e) => this.profile = e.results[0].picture.large)
      this.getData().then((e) => this.gender = e.results[0].gender)
      this.getData().then((e) => this.phone = e.results[0].phone)
    }
  }
}
</script>