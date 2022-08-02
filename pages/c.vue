<template>
    <div class=" flex md:container md:mx-auto">
        <div class="md:w-2/3 bg-lime-200">
            <h1 class="text-blue-700 font-bold text-2xl text-center"> Display User Data </h1>

            <!-- <input type="text"  @keyup="userFindByName(userName)" v-model="userName" id="userName" name="userName" placeholder="Find by Name" class="rounded-xl p-1 m-1">
            <input type="text" @keyup="userFindByEmail(userEmail)" v-model="userEmail" id="userEmail" name="userEmail" placeholder="Find by Email" class="rounded-xl p-1 m-1">
            <input type="number" @keyup="userFindByMobile(userMob)" v-model="userMob" id="userMob" name="userMob" placeholder="Find by Mob" class="rounded-xl p-1 m-1"> -->
            <input type="text" @keyup="userFindByAddress(userAddress)" v-model="userAddress" id="userName" name="userAddress" placeholder="Search for Anything" class="rounded-xl px-5 p-1 m-1">
            <table  class="w-11/12 border-1 m-3 border-stone-800">
                <!-- v-show="allUserData.length>=1" -->
                <tr class="border border-1 border-stone-800">
                    <th class="border border-1 border-stone-800">Name</th>
                    <th class="border border-1 border-stone-800">Email</th>
                    <th class="border border-1 border-stone-800">Mobile</th>
                    <th class="border border-1 border-stone-800">Address</th>
                    <th class="border border-1 border-stone-800" colspan="2">Action</th>
                    
                </tr>

                <tr v-for="(user, i) in allUserData" :key="user" >
                    <td class="border border-1 border-stone-800">{{user.name}}</td>
                    <td class="border border-1 border-stone-800">{{user.email}}</td>
                    <td class="border border-1 border-stone-800">{{user.mobile}}</td>
                    <td class="border border-1 border-stone-800">{{user.address}}</td>
                    <td class="border border-1 border-stone-800"><button @click="onEdit(i)" class="bg-black hover:bg-gray-800 p-1 px-2 rounded-lg text-white" id="edit" type="button">Edit</button></td>
                    <td class="border border-1 border-stone-800"><button @click="deleteUser(i)" class="bg-black hover:bg-red-800 p-1 px-2 rounded-lg text-white" id="delete" type="button">Delete</button></td>
                </tr>
            </table>
            <!-- <div class="bg-blue-300 md:container w-1/3" > Hello div 2 -->

            <!-- </div> -->
        </div>
        <!-- <h1>Heelo2</h1> -->
        <!-- </div> -->

        <div class="bg-blue-300  sm:w-1/3" >
            <h1 id="formName" class="text-blue sm:text-3xl item-center font-bold sm:ml-8">Add User</h1>
            <form method="post">
                <table class="ml-5 m-2 sm:item-center">
                    <!-- Name -->
                    <tr>
                        <td>
                            <label for="name">Name</label>
                        </td>
                        <td>
                            <input type="text" v-model="userData.name" name="name" id="name" placeholder="Name" class="sm:rounded-xl sm:p-1" required>
                        </td>
                    </tr>

                    <!-- Email -->
                    <tr>
                        <td>
                            <label for="email">Email</label>
                        </td>
                        <td>
                            <input type="email" v-model="userData.email" name="email" id="email" placeholder="Email" class="sm:rounded-xl sm:p-1" required>
                        </td>
                    </tr>

                    <!-- Mobile -->
                    <tr>
                        <td>
                            <label for="mobile">Mobile</label>
                        </td>
                        <td>
                            <input type="number" v-model="userData.mobile" name="mobile" id="moile" placeholder=" Mobile No." class="sm:rounded-xl mr-5 sm:p-1" required>
                        </td>
                    </tr>

                    <!-- Address -->
                    <tr>
                        <td>
                            <label for="address">Address</label>
                        </td>
                        <td>
                            <textarea name="address" v-model="userData.address" id="address" placeholder="Address" class="sm:rounded-xl sm:p-1 "  rows="3" required></textarea>
                        </td>
                    </tr>
                    <!-- Buttons -->
                    <tr>
                        <td>
                            <button @click="submitUserForm" class="bg-black hover:bg-gray-800 p-1 px-2 rounded-lg text-white" id="submit" type="submit">Submit</button>
                        </td>
                        <td>
                            <button @click="resetForm" class="bg-black hover:bg-gray-800 p-1 px-2 rounded-lg text-white" id="reset" type="reset">Reset</button>
                        </td>
                    </tr>

                </table>
            </form>

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
            // index: index + 1,
            allUserData : [],
            // i : 0,
            // show : false,
            userData : {
                
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
            console.log(this.userData);
            
            // Check Email id is unique or not
            this.uniqueEmail = this.allUserData.filter((e) => {
                if(e.email != this.userData.email){
                
                    console.log(e);
                    
                }else{
                    if(this.isEdit===true){
                        this.allUserData[this.indexEdit]=this.userData;
                    }else{
                        alert("Email Already Registered");
                        this.resetForm();
                    }
                }
            });
            
                if(this.isEdit===true){
                    this.allUserData[this.indexEdit]=this.userData;
                    this.isEdit=false;
                    this.indexEdit = -1;
               
                }
                else{
                    
                    // alert("unable to update");
                    if(this.userData.email== ''){
                            alert("Please enter unique Email Id")
                    }else{
                        this.allUserData.push(this.userData);
                    }
                }
           
            this.userData = { name:'', email:'',mobile:'',  address:'', };
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
            this.userData.name = this.allUserData[index].name;
            this.userData.email = this.allUserData[index].email;
            this.userData.mobile = this.allUserData[index].mobile;
            this.userData.address = this.allUserData[index].address;
            
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
            this.userData = { name:'',  email:'',mobile:'', address:'',};
        },
        // // Find user by Name in array
        // userFindByName(userName){         
        //     console.log(userName);
        //     this.userFound = this.allUserData.filter((e) => {
        //         // if(e.name == userName)
        //         if(e.name.startsWith(userName)){
        //             console.log(e);
        //             // if(e.name.startsWith(userName))
        //             return e;
                    
        //         }
        //     }); 
        //     console.log(this.userFound);           
        // },
        // // Find user by Email in array
        // userFindByEmail(userEmail){         
        //     console.log(userEmail);
        //     this.userFound = this.allUserData.filter((e) => {
        //         // if(e.email == userEmail)
        //         if(e.email.startsWith(userEmail)){
        //             console.log(e);
        //             return e;
        //             // alert("user Found" + e.firstName+ ""+e.lastName);
        //         }
        //     }); 
        //     console.log(this.userFound);           
        // },
        // // Find user by Mobile in array
        // userFindByMobile(userMob){         
        //     console.log(userMob);
        //     this.userFound = this.allUserData.filter((e) => {
        //         if(e.mobile == userMob){
        //         // if(e.mobile.startsWith(userMob)){
        //             console.log(e);
        //             return e;
        //             // alert("user Found" + e.firstName+ ""+e.lastName);
        //         }
        //     }); 
        //     console.log(this.userFound);           
        // },
        
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
                    // alert("user Found" + e.firstName+ ""+e.lastName);
                }
            }); 
            console.log(this.userFound);           
        },
    }
}
</script>