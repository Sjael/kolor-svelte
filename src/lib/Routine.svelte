<script>

  let routine = [];

let exercises = {
  "chest": [
    "pushups",
    "ring dips",
    "dumbbell press"
  ],
  "back": [
    "ring rows",
    "upside down hang",
    "pullups"
  ],
  "shoulders" : [
    "barbell raise",
    "lateral raise",
    "lunge row"
  ]
};

function make_routine(){
  for (const [key, value] of Object.entries(exercises)) {
    console.log(key);
    console.log(value[Math.floor(Math.random()*value.length)])
  }
}
make_routine();

let exam = {
    "chest": {
        "pushups" : 30,
        "dips" : 10,
    },
    "back": {
        "pullups" : 50,
        "ring rows" : 20,
    },
}


function weighted_random(options) {
    var i;

    var weights = [];

    for (i = 0; i < options.length; i++)
        weights[i] = options[i].weight + (weights[i - 1] || 0);
    
    var random = Math.random() * weights[weights.length - 1];
    
    for (i = 0; i < weights.length; i++)
        if (weights[i] > random)
            break;
    
    return options[i].item;
}

</script>

<button on:click="{make_routine}">click</button>
