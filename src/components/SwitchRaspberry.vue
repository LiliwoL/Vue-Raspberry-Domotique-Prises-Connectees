<template>
  <div class="switches">
    <SingleSwitch switchNumber="1" state="{{ switch_1_state }}" @myEvent="changeSwitchesState"></SingleSwitch>

    <SingleSwitch switchNumber="2" state="{{ switch_2_state }}" @myEvent="changeSwitchesState"></SingleSwitch>

    <SingleSwitch switchNumber="3" state="{{ switch_3_state }}" @myEvent="changeSwitchesState"></SingleSwitch>

    <SingleSwitch switchNumber="4" state="{{ switch_4_state }}" @myEvent="changeSwitchesState"></SingleSwitch>
  </div>
</template>

<script>
import SingleSwitch from "@/components/SingleSwitch";

export default {
  name: 'SwitchRaspberry',
  components: {
    SingleSwitch
  },
  props: {
  },

  data() {
    return {
      // Tableau contenant les switches et leur état
      switches: [],
      switches_state_uri: process.env.VUE_APP_API_ENDPOINT,

      // Switches states
      switch_1_state: 0,
      switch_2_state: 0,
      switch_3_state: 0,
      switch_4_state: 0,
    };
  },

  // Methods
  methods: {
    /**
     * Récupère l'état de tous les switches
     * https://www.koderhq.com/tutorial/vue/http-fetch/#fetch-method
     *
     * @returns {Promise<void>}
     */
    async getSwitchesState() {
      try {
        const response = await fetch(
            this.switches_state_uri,
            {
              method: 'POST',
              headers: {
                'Accept': 'application/json',
                'Content-Type': 'application/json'
              },
              body: JSON.stringify({api_key: 'raspB3rr1'})
            }
        );

        const content = response.json();

        // JSON responses are automatically parsed.
        this.switches = content;

        // Change les états des switches
        this.changeSwitchesState();
      }
      catch(error){
        console.log(error);
      }
    },

    changeSwitchesState( content ){
      if (content){
        // Si on reçoit depuis un élément enfant

        // Creates variable name1
        let variable_name = 'switch_' + this.content.Prise + '_state';
        this[variable_name] = this.content.state;

      }else{
        //1 Parcours du tableau des switches
        this.switches.forEach( switchCurrent => {
          // Creates variable name
          let variable_name = 'switch_' + switchCurrent.Prise + '_state';
          this[variable_name] = switchCurrent.state;
        })
      }
    }
  },
  // Méthodes exécutées au démarrage de l'appli
  mounted() {
    // Récupération des variables d'environnement
    console.log("Env");
    console.log(process.env.VUE_APP_API_ENDPOINT)
    console.log(process.env.VUE_APP_API_KEY);

    // Récupération des états des prises
    this.getSwitchesState();
  }
}
</script>

<style>
.switch {
  background-color: black;
  width: 150px;
  height: 195px;
  box-shadow: 0 0 10px 2px rgba(0, 0, 0, 0.2), 0 0 1px 2px white, inset 0 2px 2px -2px white, inset 0 0 2px 15px grey, inset 0 0 2px 22px white;
  border-radius: 5px;
  padding: 20px;
  perspective: 700px;
}
.switch input {
  display: none;
}
.switch input:checked + .button {
  transform: translateZ(20px) rotateX(25deg);
  box-shadow: 0 -10px 20px #ff1818;
}
.switch input:checked + .button .light {
  animation: flicker 0.2s infinite 0.3s;
}
.switch insert:checked + .button .shine {
  opacity: 1;
}
.switch input:checked + .button .shadow {
  opacity: 0;
}
.switch .button {
  transition: all 0.3s cubic-bezier(1, 0, 1, 1);
  transform-origin: center center -20px;
  transform: translateZ(20px) rotateX(-25deg);
  transform-style: preserve-3d;
  background-color: #9b0621;
  width: 100%;
  height: 100%;
  position: relative;
  cursor: pointer;
  background: linear-gradient(#980000 0%, #6f0000 30%, #6f0000 70%, #980000 100%);
  background-repeat: no-repeat;
}
.switch .button::before {
  content: "";
  background: linear-gradient(rgba(255, 255, 255, 0.8) 10%, rgba(255, 255, 255, 0.3) 30%, #650000 75%, #320000) 50% 50%/97% 97%, #b10000;
  background-repeat: no-repeat;
  width: 100%;
  height: 50px;
  transform-origin: top;
  transform: rotateX(-90deg);
  position: absolute;
  top: 0;
  left: 0;
}
.switch .button::after {
  content: "";
  background-image: linear-gradient(#650000, #320000);
  width: 100%;
  height: 50px;
  transform-origin: top;
  transform: translateY(50px) rotateX(-90deg);
  position: absolute;
  bottom: 0;
  left: 0;
  box-shadow: 0 50px 8px 0px black, 0 80px 20px 0px rgba(0, 0, 0, 0.5);
}
.switch .light {
  opacity: 0;
  animation: light-off 1s;
  position: absolute;
  width: 100%;
  height: 100%;
  background-image: radial-gradient(#ffc97e, #ff1818 40%, transparent 70%);
}
.switch .dots {
  position: absolute;
  width: 100%;
  height: 100%;
  background-image: radial-gradient(transparent 30%, rgba(101, 0, 0, 0.7) 70%);
  background-size: 10px 10px;
}
.switch .characters {
  position: absolute;
  width: 100%;
  height: 100%;
  background: linear-gradient(white, white) 50% 20%/5% 20%, radial-gradient(circle, transparent 50%, white 52%, white 70%, transparent 75%) 50% 80%/33% 25%;
  background-repeat: no-repeat;
}
.switch .shine {
  transition: all 0.3s cubic-bezier(1, 0, 1, 1);
  opacity: 0.3;
  position: absolute;
  width: 100%;
  height: 100%;
  background: linear-gradient(white, transparent 3%) 50% 50%/97% 97%, linear-gradient(rgba(255, 255, 255, 0.5), transparent 50%, transparent 80%, rgba(255, 255, 255, 0.5)) 50% 50%/97% 97%;
  background-repeat: no-repeat;
}
.switch .shadow {
  transition: all 0.3s cubic-bezier(1, 0, 1, 1);
  opacity: 1;
  position: absolute;
  width: 100%;
  height: 100%;
  background: linear-gradient(transparent 70%, rgba(0, 0, 0, 0.8));
  background-repeat: no-repeat;
}

@keyframes flicker {
  15% {
    opacity: 1;
  }
  80% {
    opacity: 0.8;
  }
  100% {
    opacity: 1;
  }
}
@keyframes light-on 100% {
0% {
  opacity: 1;
}
80% {
  opacity: 0;
}
}
</style>