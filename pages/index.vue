<template>
  <div >
    <div class="bg-amber-700">
      <form>
      <h1 style="color: red" class="font-bold text-3xl p-6"></h1>

      <input type="text" @keyup="userFindByAddress(userAddress)" v-model="userAddress" id="userName" name="userAddress" placeholder="Search for Anything" class="rounded-xl px-5 p-1 m-1">


      <br /> <br />
      Name:<input
        type="text"
        class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3"
        v-model="user.name" name="name" id="name" placeholder="Name" required
      /><br /><br />

      Email:<input
        type="email"
        class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3"
        v-model="user.email" name="email" id="email" placeholder="Email" required
      /><br /><br />

      Mobile:<input
        type="text"
        class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3"
        v-model="user.mobile" name="mobile" id="mobile" placeholder=" Mobile No."  max="10" required
      /><br /><br />

      Address:<input
        type="text"
        class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-3"
        name="address" v-model="user.address" id="address" placeholder="Address" required
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
      


      <table  id="list">
        <tr>
          <!-- <th class="px-4 border-black rounded-lg border-2">id</th> -->
          <th class="px-4 border-blue-400 rounded-lg border-2">Name</th>
          <th class="px-4 border-blue-400 rounded-lg border-2">Email</th>
          <th class="px-4 border-blue-400 rounded-lg border-2">Mobile</th>
          <th class="px-4 border-blue-400 rounded-lg border-2">Address</th>
          <th class="px-4 border-blue-400 rounded-lg border-2">Action</th>
        </tr>
        <tr
         v-for="(user, i) in allUserData" :key="user"
        >
          <!-- <td class="px-4 border-black rounded-lg border-2">{{item.id=i+1}}</td> -->
          <td class="px-4 border-blue-400 rounded-lg border-2">
            {{ user.name }}
          </td>
          <td class="px-4 border-blue-400 rounded-lg border-2">
            {{ user.email }}
          </td>
          <td class="px-4 border-blue-400 rounded-lg border-2">
            {{ user.mobile }}
          </td>
          <td class="px-4 border-blue-400 rounded-lg border-2">
            {{ user.address }}
          </td>
          <td class="px-4 border-blue-400 rounded-lg border-2">
            {{ user.Action }}
            <button
              class="mx-3 rounded-lg bg-red-400 hover:bg-red-600 text-white w-20"
              @click="deleteUser(i)"
            >
              Delete
            </button>
            <button
              class="mx-3 rounded-lg bg-green-400 hover:bg-green-600 text-white w-20"
              @click="onEdit(i)"
            >
              Edit
            </button>
          </td>
        </tr>
      </table>


    </div>
  </div>






<hr class=" mt-4 border-4 border-orange-600">
    <div>
        <table  class="w-full border-1 m-3 border-stone-800">
                <!-- v-show="allUserData.length>=1" -->
                <tr class="border border-1 border-stone-800">
                    <th class="border border-1 border-stone-800">Name</th>
                    <th class="border border-1 border-stone-800">Email</th>
                    <th class="border border-1 border-stone-800">Mobile</th>
                    <th class="border border-1 border-stone-800">Address</th>
                    <!-- <th class="border border-1 border-stone-800" colspan="2">Action</th> -->
                    
                </tr>

                <tr v-for="item in userFound" :key="item" >
                    <td class="border border-1 border-stone-800">{{item.name}}</td>
                    <td class="border border-1 border-stone-800">{{item.email}}</td>
                    <td class="border border-1 border-stone-800">{{item.mobile}}</td>
                    <td class="border border-1 border-stone-800">{{item.address}}</td>
                    <!-- <td class="border border-1 border-stone-800"><button @click="onEdit(i)" class="bg-black hover:bg-gray-800 p-1 px-2 rounded-lg text-white" id="edit" type="button">Edit</button></td> -->
                    <!-- <td class="border border-1 border-stone-800"><button @click="deleteUser(i)" class="bg-black hover:bg-red-800 p-1 px-2 rounded-lg text-white" id="delete" type="button">Delete</button></td> -->
                </tr>
            </table>
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
            console.log(this.user)




            this.emailMatch = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
                // if(this.userData.email.matchAll(this.emailMatch)){
                if(this.emailMatch.test(this.user.email)){
                    // alert("Email is valid");
                    // console.log("Email is valid");
                }else{
                    alert("Email is Invalid");
                    this.resetForm();
                }
            // Validation for Email
if (isNaN(this.user.mobile) || this.user.mobile < 1000000000 || this.user.mobile > 9999999999) {
                alert("Mobile Number is Invalid");
                this.resetForm();
            } else {
                // alert("Mobile Number is valid");
            }
            //   // Validation for Address
            // if(this.userData.address!=''){
                if(this.user.address==null || this.user.address==""){
                    alert("Please Enter Address");
                    // console.log("Please Enter Address");
                    this.resetForm();
            }else{
                    // alert("Address is valid");
            }
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
                    
                    //alert("unable to update");
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
        userFindByAddress(userAddress){
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
                    
                }
            });
            console.log(this.userFound);
        },
    },
    
}
</script>