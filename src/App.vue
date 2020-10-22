<template>
  <div id="app" class="container">

      <h3>
          This is a simple school application!
      </h3>
      <h5>
        <router-link to="/">Home</router-link>
      </h5>
      <h6>
        <router-link to="/student-form">Student form | </router-link>
        <router-link to="/course-form">Course form | </router-link>
        <router-link to="/mark-form">Mark form</router-link>
      </h6>

      

    <div class="row">
      <!-- Student section -->

      <div class="col-xl-4 col-md-6 col-sm-6">
        <p>Students</p>

        <!-- Form -->
        <router-view>
          <form action="" slot="s">
            <input type="text" v-model="students.fullname" placeholder="Full name">
            <button class="btn btn-outline-primary" @click.prevent="add_student">Add student</button>
          </form>
        </router-view>

        

        <!-- <app-studform>
          <form action="" slot="s">
            <input type="text" v-model="students.fullname" placeholder="Full name">
            <button class="btn btn-outline-primary" @click.prevent="add_student">Add student</button>
        </form>
        </app-studform> -->


        <!-- List -->

        <app-studlist v-if="allStud!='' ">
          <div slot="sl">
            <table class="table">
              <thead>
                <tr>
                  <th colspan="4" scope="col">List of all students</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(i,index) in allStud">
                  <td>{{ i }}</td>
                  <td id="sd" @click="deletestud(index)">Delete</td>
                  <td id="su">Update</td>
                </tr>
              </tbody>
          </table>
          </div>
        </app-studlist>

      </div>

      <!-- End of Student section -->

      <!-- Course section -->

      <div class="col-xl-4 col-md-6 col-sm-6">
        <p>Courses</p>

        <!-- Form -->
        <router-view>
          <form action="" slot="c">
            <input type="text" v-model="courses.name" placeholder="Course name">
            <button class="btn btn-outline-primary" @click.prevent="add_course">Add course</button>
        </form>
        </router-view>

        <!-- <app-courseform>
          <form action="" slot="c">
            <input type="text" v-model="courses.name" placeholder="Course name">
            <button class="btn btn-outline-primary" @click.prevent="add_course">Add course</button>
        </form>
        </app-courseform> -->

        <!-- List -->

        <app-courselist v-if="allCourse!='' ">
          <div slot="cl">
            <table class="table">
              <thead>
                <tr>
                  <th colspan="4" scope="col">List of all courses</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(i,index) in allCourse">
                  <td>{{ i }}</td>
                  <td id="sd" @click="deletecourse(index)">Delete</td>
                  <td id="su">Update</td>
                </tr>
              </tbody>
          </table>
          </div>
        </app-courselist>

      </div>

      <!-- End of course section -->

      <!-- Marks section -->

      <div class="col-xl-4 col-md-6 col-sm-6">
        <p>Marks</p>
        <router-view>
          <form action="" slot="m">
            <select v-model="selectedstudent">
              <option v-for="(i,index) in allStud">{{ i }}</option> <br>
            </select> 

            <select v-model="selectedcourse">
              <option v-for="(i,index) in allCourse">{{ i }}</option> <br>
            </select>

            <select v-model="selectedmark">
              <option v-for="i in 100">{{ i }}%</option>
            </select> <br>

            <button class="btn btn-outline-primary" @click.prevent="add_mark">Add mark</button>
          </form>
        </router-view>

        <!-- <app-markform>
          <form action="" slot="m">
            <select v-model="selectedstudent">
              <option v-for="(i,index) in allStud">{{ i }}</option> <br>
            </select> 

            <select v-model="selectedcourse">
              <option v-for="(i,index) in allCourse">{{ i }}</option> <br>
            </select>

            <select v-model="selectedmark">
              <option v-for="i in 100">{{ i }}%</option>
            </select> <br>

            <button class="btn btn-outline-primary" @click.prevent="add_mark">Add mark</button>
          </form>
        </app-markform> -->

        <app-marklist v-if="allMarks!='' ">
          <div slot="ml">
            <table class="table">
              <thead>
                <tr>
                  <th colspan="4" scope="col">List of all marks</th>
                </tr>
                <tr>
                  <th scope="col">Mark</th>
                  <th scope="col">Delete</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(i,index) in allMarks">
                  <td>{{ i }}</td>
                  <td id="sd" @click="deletemark(index)">Delete</td>
                </tr>
              </tbody>
          </table>

          </div>
        </app-marklist>

      </div>

      <!-- End of marks section -->

    </div>
  </div>
</template>

<script>

import Studform from './components/Studform.vue';
import Courseform from './components/Courseform.vue';
import Markform from './components/Markform.vue';
import Studlist from './components/Studlist.vue';
import Courselist from './components/Courselist.vue';
import Marklist from './components/Marklist.vue';

import about from './components/about.vue';

export default {
    data(){
        return{
            students:{
                fullname:''
            },
            courses:{
              name:''
            },
            marks:{
              selectedmark:'',
              selectedstudent:'',
              selectedcourse:''
            },
            
            allStud:[],
            allCourse:[],
            allMarks:[],
            isSent:false,
        }
      },
      methods:{
          add_student(){
              // var selectedstud = this.allStud[i];
              this.isSent = true;
              if(this.students.fullname == ""){
                  alert("Some field is empty !");
              }else{
              this.allStud.push(this.students.fullname);
              this.students.fullname = '';
              }
          },
          add_course(){
              this.isSent = true;
              if(this.courses.name == ""){
                  alert("Some field is empty !");
              }else{
              this.allCourse.push(this.courses.name);
              this.courses.name = '';
              }
          },
          add_mark(){
              this.isSent = true;
              
              this.allMarks.push(this.selectedstudent+' '+this.selectedcourse+' '+this.selectedmark);
              this.selectedstudent = '', this.selectedcourse = '', this.selectedmark = ''
              
          },
          deletestud(i){
            this.allStud.splice(i,1);
          },
          deletecourse(i){
            this.allCourse.splice(i,1);
          },
          deletemark(i){
            this.allMarks.splice(i,1);
          }
      }
      ,components:{
          'app-studform':Studform,
          'app-courseform':Courseform,
          'app-studlist':Studlist,
          'app-courselist':Courselist,
          'app-markform':Markform,
          'app-marklist':Marklist,
          'app-about':about,
      }
}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000000;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

#sd{
    color: red;
}
#su{
  color: green;
}
#sg{
  color: blue;
}
</style>
