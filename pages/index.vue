<template>
  <div class="  w-2/3 grid gap-x-7  grid-cols-2 h-screen" >
    <div class="bg-amber-700">
      <form>
      <h1 style="color: red" class="font-bold text-3xl p-6"></h1>
      <!-- ID:<input
        type="number"
        class="bg-white border border-slate-300 rounded-md mx-4 py-2 pl-9 pr-3"
        v-model="signUp.id"
      /><br /><br /> -->
      Name:<input
        type="text"
        class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3"
        v-model="Table.name"
      /><br /><br />

      Email:<input
        type="email"
        class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3"
        v-model="Table.email"
      /><br /><br />

      Mobile:<input
        type="text"
        class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3"
        v-model="Table.mobile"
      /><br /><br />

      Address:<input
        type="text"
        class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3"
        v-model="Table.Address"
      /><br /><br />

      


      
      <button
        type="button"
        id="submit-button"
        class="
          border-solid
          rounded
          border-2 border-indigo-600
          p-3
          bg-gradient-to-r
          from-indigo-500
          via-purple-500
          to-pink-500
        "
        v-on:click="submitFormValues()"
      >
        Submit
      </button>
      </form>
    </div>
    <div class="bg-gray-300 col-span-2">
      <table class=" border-black-400 border-separate bg-white  border border-slate-400 m-20" >
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Email</th>
          <th>Mobile</th>
          <th>Address</th>

          <th colspan="2">Action</th>
        </tr>
        <tr v-for="(user, index) in users" :key="user">
          <td>{{ index + 1 }}</td>
          <td>{{ user.name }}</td>
                    <td>{{ user.email }}</td>
                              <td>{{ user.mobile }}</td>

                                                  <td>{{ user.address}}</td>



          <td>
            <button
              class="
                border-solid
                rounded
                border-2 border-indigo-600
                p-1
                bg-gradient-to-r
                from-indigo-500
                via-purple-500
                to-pink-500
              "
              v-on:click="editCliked(index)"
            >
              Edit
            </button>
          </td>
          <td>
            <button
              class="
                border-solid
                rounded
                border-2 border-indigo-600
                p-1
                bg-gradient-to-r
                from-indigo-500
                via-purple-500
                to-pink-500
              "
              @click="deleteClicked(index)"
            >
              Delete
            </button>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>
<script>
export default {
  name: "index",
  data() {
    return {
      isEdit: false,
      editIndex: -1,
      users: [],
      Table: {
        id: null,
        name: null,
        email: "",
        mobile:"",
        Address:"",
      
      },
    };
  },
  methods: {
    submitFormValues() {
      if (this.isEdit === true) {
        this.users[this.editIndex] = this.Table;
        (this.isEdit = false), (this.editIndex = -1);
        let b = document.getElementById("submit-button");
        b.innerText = "Submit";
      } else {
        this.users.push(this.Table);
      }
      console.warn(this.Table);
      console.log(this.users);
      this.Table = {
        id: "",
        name: "",
        email: "",
        mobile:"",
        Address:""
        
      };
    },
    editCliked(i) {
      console.log("Edit");
      this.Table.id = this.users[i].id;
      this.Table.name = this.users[i].name;
      this.Table.email = this.users[i].email;
            this.Table.mobile = this.users[i].mobile;
                  this.Table.Address = this.users[i].Address;


      
      this.isEdit = true;
      this.editIndex = i;
      let b = document.getElementById("submit-button");
      b.innerText = "Update";
    },
    deleteClicked(index) {
      console.log("delete");
      this.users.splice(index, 1);
    },
  },
};
</script>