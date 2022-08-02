<template>
  <div >
    <div class="bg-amber-700">
      <form>
      <h1 style="color: red" class="font-bold text-3xl p-6"></h1>


<!-- <input type="text"  @keyup="userFindByName(userName)" v-model="userName" id="userName" name="userName" placeholder="Find by Name" class="rounded-xl p-1 m-1">
            <input type="text" @keyup="userFindByEmail(userEmail)" v-model="userEmail" id="userEmail" name="userEmail" placeholder="Find by Email" class="rounded-xl p-1 m-1">
            <input type="number" @keyup="userFindByMobile(userMob)" v-model="userMob" id="userMob" name="userMob" placeholder="Find by Mob" class="rounded-xl p-1 m-1">--->
            <input type="text" @keyup="userFindByAddres(userAddress)" v-model="userAddress" id="userName" name="userAddress" placeholder="Find by Address" class="rounded-xl p-1 m-1"> 
                  <input type="text" @keyup="userFindByAddress(userAddress)" v-model="userAddress" id="userName" name="userAddress" placeholder="Search for Anything" class="rounded-xl px-5 p-1 m-1">


      <br /> <br />
      Name:<input
        type="text"
        class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3"
        v-model="user.name" name="name" id="name" placeholder="Name"
      /><br /><br />

      Email:<input
        type="email"
        class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3"
        v-model="user.email" name="email" id="email" placeholder="Email"
      /><br /><br />

      Mobile:<input
        type="text"
        class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3"
        v-model="user.mobile" name="mobile" id="moile" placeholder=" Mobile No."
      /><br /><br />

      Address:<input
        type="text"
        class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3"
        name="address" v-model="user.address" id="address" placeholder="Address"
      /><br /><br />

      


      
      <button

      @click="submitUserForm"
        type="button"
        id="submit"
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
        v-on:click="submitUserForm()"
      >
        Submit
      </button>
      </form>
    </div>
    <div class="bg-gray-300 col-span-2">
      <table class=" border-black-400 border-separate bg-white  border border-slate-400 m-20" >
        <tr v-for="(user, i) in allUserData" :key="user" >
                    <td class="border border-1 border-stone-800">{{user.name}}</td>
                    <td class="border border-1 border-stone-800">{{user.email}}</td>
                    <td class="border border-1 border-stone-800">{{user.mobile}}</td>
                    <td class="border border-1 border-stone-800">{{user.address}}</td>
                    <td class="border border-1 border-stone-800"><button @click="onEdit(i)" class="bg-black hover:bg-gray-800 p-1 px-2 rounded-lg text-white" id="edit" type="button">Edit</button></td>
                    <td class="border border-1 border-stone-800"><button @click="deleteUser(i)" class="bg-black hover:bg-red-800 p-1 px-2 rounded-lg text-white" id="delete" type="button">Delete</button></td>
                </tr>
      </table>
    </div>
  </div>
</template>
<script>
export default {
    data(){
        
        return{
            isEdit: false,
            indexEdit : -1,
            userName: '',
            userEmail: '',  
            userMob: '',
            userAddress: '',
            userFound: [],
            uniqueEmail:[],
            address1: '',
            address2: '',
            name1:'',
            name2:'',
            email1:'',
            email2:'',
            mobile1:'',
            mobile2:'',
          
            allUserData : [],
            
            user : {
                
                name : '',
                email : '',
                mobile : '',
                address : '',
                
            },
        }
    },
    methods: {
        submitUserForm(event){
            event.preventDefault(event);
            console.log(this.user);
            
            // Check Email id is unique or not
            this.uniqueEmail = this.allUserData.filter((e) => {
                if(e.email != this.user.email){
                
                    console.log(e);
                    
                }else{
                    if(this.isEdit===true){
                        this.allUserData[this.indexEdit]=this.user;
                    }else{
                        alert("Email Already Registered");
                        this.resetForm();
                    }
                }
            });
            
                if(this.isEdit===true){
                    this.allUserData[this.indexEdit]=this.user;
                    this.isEdit=false;
                    this.indexEdit = -1;
               
                }
                else{
                    
                    // alert("unable to update");
                    if(this.user.email== ''){
                            alert("Please enter unique Email Id")
                    }else{
                        this.allUserData.push(this.user);
                    }
                }
           
            this.user = { name:'', email:'',mobile:'',  address:'', };
            console.log(" User Form Values", this.allUserData);
            const formHead = document.getElementById('formName');
            formHead.innerText = 'Add User';
            const myButton = document.getElementById('submit');
            myButton.innerText = 'Submit';
        },
        //  Edit User Data
        onEdit(index){
            console.log(this.allUserData[index]);
            // console.log(this.allUserData[this.index]);
            this.user.name = this.allUserData[index].name;
            this.user.email = this.allUserData[index].email;
            this.user.mobile = this.allUserData[index].mobile;
            this.user.address = this.allUserData[index].address;
            
            const formHead = document.getElementById('formName');
            formHead.innerText = 'Edit User';
            const myButton = document.getElementById('submit');
            myButton.innerText = 'Update';
            this.isEdit=true;
            this.indexEdit = index;
            
        },
        // Delete user from array
        deleteUser(index){
            console.log(index);
            this.allUserData.splice(index, 1);
            const formHead = document.getElementById('formName');
            formHead.innerText = 'Add User';
            const myButton = document.getElementById('submit');
            myButton.innerText = 'Submit';
        },  
        // reset form values
        resetForm() {
            console.log("reset call");
            const formHead = document.getElementById('formName');
            formHead.innerText = 'Add User';
            const myButton = document.getElementById('submit');
            myButton.innerText = 'Submit';
            // indexOfEdit=-1;
            this.isEdit=false;
            this.user = { name:'',  email:'',mobile:'', address:'',};
        },
        
        
        // Find user by Address in array
        userFindByAddres(userAddress){         
            console.log(userAddress);
            this.userFound = this.allUserData.filter((e) => {
                // if(e.address == userAddress)
                this.address1 = userAddress.toLocaleLowerCase();
                console.log(this.address1);
                this.address2 = e.address.toLocaleLowerCase();
                this.name1 = userAddress.toLocaleLowerCase();
                this.name2 = e.name.toLocaleLowerCase();
                this.email1 = userAddress.toLocaleLowerCase();
                this.email2 = e.email.toLocaleLowerCase();
                this.mobile1 = userAddress.toString();
                this.mobile2 = e.mobile.toString();
                if(this.address2.startsWith(this.address1) || this.name2.startsWith(this.name1) || this.email2.startsWith(this.email1) || this.mobile2.startsWith(this.mobile1)  ){
                    // toLocaleLowerCase
                    console.log(e);
                    return e;
                    // alert("user Found" + e.firstName+ ""+e.lastName);
                }
            }); 
            console.log(this.userFound);           
        },

        userFindByAddress(userName){
            console.log(userName);
            this.userFound = this.users.filter((e) => {
                // if(e.name == userName)
                if(e.fname.startsWith(userName)){
                    console.log(e);
                    // if(e.name.startsWith(userName))
                    return e;
                    // alert("user Found" + e.firstName+ ""+e.lastName);
                }
            });
            console.log(this.userFound);
        },
    },
    }
}
</script>