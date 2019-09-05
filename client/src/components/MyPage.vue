<template>
 <div id="body">
   <h1>
     Chitthi
   </h1>

   <img class="robo" src="../../src/assets/yellowrobo.jpg">

   <h6 >
     Hi! I am your Personal RA. No judgments only solution.
   </h6>


   <input class="info" type="text" name="utterance" v-model="utterance" placeholder="Hello Buddy! Can I help you? " id="inputfield">
   <button @click="register" class="btn">Send</button>
   <button @click="clear" class="btn">Clear</button>

<div v-if="results === 'HealthIssues'">
  <h6 class="answer">  Oh no! So, you're sick? It's okay. Take three deep breathes.
    Things could've been worse.


    <li>
      Call your parents. Sometimes, just talking to them makes us feel better.
    </li>
    <li>
      Go to the University Health Center. It's just 10 minutes of walk and there is almost no wait time.
    </li>
    <li>
      Don't forget to eat. I know students sometimes forget to eat because of class load and all other activities. Don't do that to yourself.
    </li>
    <li>
     Keep your friends updated. You're far away from family so its important you've got someone who will be there when you need them.
    </li>

  </h6>


</div>
<div v-else-if="results === 'MentalHealthIssues'">
   <h6 class="answer">  I feel you! College can be overwhelming and stressful.
 Here are some things that helped me personally to deal with my emotions.

     <li>
       Talk to a counselor. We have free counselling session on campus. Sometimes we just need someone to talk to.
     </li>
     <li>
       Practice mindfulness exercise. It's scientifically proven that it helps.
     </li>
     <li>
       Strengthen your social connections. Put time and energy into meeting new people and developing friendships.
     </li>
     <li>
       Don't think you're less than anybody else. You can achieve anything you want to.
     </li>

   </h6>

  <h6>Some useful links:</h6>
    <div class="popups">
      <a href="https://campusrec.olemiss.edu/group-fitness/" target="_blank">
      <img class="pop" src="../../src/assets/yoga.png" >
      </a>
      <a href="https://counseling.olemiss.edu/" target="_blank">
      <img class="pop" src="../../src/assets/counselling.png" alt="">
      </a>
      <a href="https://www.olemissasb.org/" target="_blank">
      <img class="pop" src="../../src/assets/saa.png" alt="">
      </a>
     </div>
    </div>

 <div v-else-if="results === 'RoommateConflicts'">



   <h6 class="answer">  <p class="bold">Trust me. You're not the only one.</p>

     <li>
       Maintain a constant stream of communication. If your roommate does something that gets on your nerves, bring it up. Chances are, they’ll be more than willing to accommodate you. Don’t let the little things add up to big things. I guarantee you, they aren’t worth it.
     </li>
     <li>
       If your roommate does something in your shared space that makes you uncomfortable, don’t back down and let that continue. Be assertive, be strong and let them know that whatever they’re doing isn’t okay with you.     </li>
     <li>
       Don’t paint a portrait of yourself as a victim and your roommate as a villain. Accept and acknowledge your role in any roommate dilemmas and take responsibility for your errors.

     </li>
     <li>
       Go to your RA! A real one ;) It’s their job to help you handle conflicts.      </li>

   </h6>


</div>
 <div v-else-if="results === 'Classload'">



     <h6 class="answer">  <p class="bold">Stay afloat. Academic anxiety is increasing</p>

       <li>
         College is not easy. It takes so much more work than high school did, but with a little determination and few tips form the list above, you will be top of the class in no time.
       </li>
       <li>
         Always know when your assignments and quizzes are due. Work ahead to keep yourself from ever getting behind. It is so easy to get behind, but so hard to get caught back up.

       </li>
       <li>
         It is important to set a realistic goal for each semester. Always set the bar high, but not so high that it can’t be attained. Reward yourself in some way for reaching the goal and then keep going!    </li>

     </h6>


</div>
   <div v-else-if="results === 'SexualAbuse'">
     <h6 class="answer">
       <p class="bold">First of all, Thanks for sharing it to me.</p>
       <p class="bold">Stay strong! It hurts my heart to see that you had to go through that. </p>
    <li>Among undergraduate students, 23.1% of females and 5.4% of males experience rape or sexual assault through physical force, violence, or incapacitation. </li>
    <li>Your safety is important. Seek physical and emotional safety, and if you’re unsure of your safety, reach out to someone you trust to help you find a place you can be safe, both in the short- and long-term.</li>
     <li>What happened is not your fault. Something happened to you that you did not want to happen. If someone is blaming you, pull away from them if possible and find non-judgmental support from people who see and believe you.</li>
<li>The Title IX coordinator at the University of Mississippi is Honey Ussery and can be reached at TitleIX@olemiss.edu, 662-915-7045 or in Martindale 270D</li>

     </h6>




   </div>



   <div v-else-if="results !== ''">
     <h6 class="answer">
       Sorry! I am still learning this language and don't really understand what you mean.
     </h6>
   </div>







 </div>
</template>

<script>

import axios from 'axios';
import "../../src/assets/css/main.css";
import 'bootstrap-vue/dist/bootstrap-vue.css';


export default {
  data()  {
      return {
          results: '',
          utterance: '',
          topScoringIntent:''
      }
  }

  ,
    methods: {
        register() {
            console.log("register button was clicked", this.utterance)
            this.callAPI(this.utterance);
        },
        callAPI(query) {
            axios.get("https://centralus.api.cognitive.microsoft.com/luis/v2.0/apps/a85465d9-f001-4775-8c75-d046847855d1?spellCheck=true&bing-spell-check-subscription-key=%7BYOUR_BING_KEY_HERE%7D&verbose=true&timezoneOffset=-360&subscription-key=fbced629668540baa786c3e2d33ae8e6&q="+query)
                .then(response =>

                {this.results = response.data.topScoringIntent["intent"]}

                )


        },
        clear(){
            this.utterance='';
        }
        }


}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #body{
    background-color: slateblue;
    width:100%;
    height:1200px;
    top:0;
  }
  #inputfield{
    font-size:12px;
  }
  h6{
    color:white;
    font-size: 15px;
  }
  h1{
    padding: 70px 0 0 0;
    color: white;
  }
  .robo{
    width:70px;
    height:70px;
    border-radius:50%;
  }
  .info{
    border: 2px solid orange;
    width: 300px;
    border-radius: 50px 50px 15px;
    padding:20px;
  }
  .btn{
    border: 2px solid white;
    width: 50px;
    margin-left: 20px;

  }
  .btn:hover{
    background-color: orange;
  }
  .answer{
    margin-left: 400px;
    top: 50px;
    margin-top: 50px;
    border: 2px solid orange;
    width: 550px;
    heigtht: 500px;
    border-radius: 50px 50px 50px 15px;
    padding: 20px;
    background-color: white;
    color: black;
    font-weight: normal;
    text-align: center;
  }
  .pop{
    width:80px;
    height:80px;
    border-radius: 50%;
    margin-left: 20px;
  }
  .pop:hover{
    cursor: pointer;
    opacity: 0.5;
  }
.bold{
  font-weight: bold;
}
</style>
