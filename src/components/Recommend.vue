<template>
    <div>
        <h1 v-if="gotd" id="gotd">Game of the Day</h1>
        <div class="pic">
            <img id="image" />
            <span class="imgtext">
                <h1 id="title"></h1>
                <p id="description"></p>
                <div id="link-container">
                <a id="link">Visit Now!</a>
                </div>
            </span>
        </div>
        <div class="center"><button type="button" @click="getGame">Recommend a game!</button></div>
    </div>
</template>


<script>
import axios from "axios";
export default {
    name: "recommend",
    data () {
        return {
            info: null,
            options: {
                method: 'GET',
                url: 'https://free-to-play-games-database.p.rapidapi.com/api/games',
                headers: {
                    'x-rapidapi-host': 'free-to-play-games-database.p.rapidapi.com',
                    'x-rapidapi-key': '7c3ae5b994msh6f81b671a5a1b76p1fdbcajsn13587eab6d90'
                }
            },
            gotd: true
        }
    },
    mounted () {
        axios.request(this.options)
        .then(response => {
            this.info = response.data;

            var now = new Date();
            var start = new Date(now.getFullYear(), 0, 0);
            var diff = (now - start) + ((start.getTimezoneOffset() - now.getTimezoneOffset()) * 60 * 1000);
            var oneDay = 1000 * 60 * 60 * 24;
            var day = Math.floor(diff / oneDay) - 1;

            var title = document.getElementById("title");
            var description = document.getElementById("description");
            var link = document.getElementById("link");
            var image = document.getElementById("image");

            image.src = response.data[day].thumbnail;
            title.innerText = response.data[day].title;
            description.innerText = response.data[day].short_description;
            link.href = response.data[day].game_url;
        })
        .catch(function (error) {
            console.error(error);
        })
        
    },
    methods: {
        getGame() {
            this.gotd = false;
            var min = Math.ceil(0);
            var max = Math.floor(365);
            var id = Math.floor(Math.random() * (max - min) + min);
            console.log(id);

            var title = document.getElementById("title");
            var description = document.getElementById("description");
            var link = document.getElementById("link");
            var image = document.getElementById("image");

            image.src = this.info[id].thumbnail;
            title.innerText = this.info[id].title;
            description.innerText = this.info[id].short_description;
            link.href = this.info[id].game_url;
        },
    },
};
</script>


<style lang="scss" scoped>
div {
    h1 {
        margin-top: 1%;
        text-align: center;
        
    }

    .center {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 1%;

        button {
            font-size: 2vw;
        }
    }
}

#gotd {
    font-size: 4vw;
}

h1,
p {
  margin: 0;
  padding: 0;
}

.imgtext {
  color: white;
  opacity: 0;
  -webkit-transition: all 300ms ease-in-out;
  -o-transition: all 300ms ease-in-out;
  transition: all 300ms ease-in-out;

  margin: 0;
  padding: 1%;
  position: absolute;
  top: 50%;
  left: 50%;
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  font-size: 2vw;

  border: 1px solid black;
  border-radius:20%;
  background-color: black;

  #description {
    text-align:center;
  }
}

#link-container {
    text-align:center;
}
a {
    color:white;
}
a:link {
    color:white;
}
a:hover {
    background-color:grey;
}

.pic {
  position: relative;
  overflow: hidden;
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 100%;
  img {
      display: block;
      margin-left: auto;
      margin-right: auto;
      width: 100%;
  }
}

.pic:hover img {
  -webkit-transition: all 300ms ease-in-out;
  -o-transition: all 300ms ease-in-out;
  transition: all 300ms ease-in-out;
  -webkit-filter: blur(2px);
  -moz-filter: blur(2px);
  -ms-filter: blur(2px);
  -o-filter: blur(2px);
  filter: blur(2px);
  transform: scale(1.03);
}

.pic:hover .imgtext {
  -webkit-opacity: 1;
  opacity: 1;
}
</style>