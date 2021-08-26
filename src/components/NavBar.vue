<template>
  <header>
    <div class="logo">
      <transition name="appear">
        <a
          href="#info"
          v-if="!Toggle"
          v-smooth-scroll
          :class="Toggle ? 'nav__logo__mobile' : 'nav__logo'"
          >Kuo</a
        ></transition
      >
    </div>
    <transition name="fade">
      <nav class="nav" v-if="desktop">
        <div class="nav__menu" id="nav-menu">
          <ul :class="Toggle ? 'nav__list__mobile' : 'nav__list'">
            <li :class="Toggle ? 'nav__link__mobile' : 'nav__link'">
              <a href="#info" v-smooth-scroll>Home</a>
            </li>
            <li :class="Toggle ? 'nav__link__mobile' : 'nav__link'">
              <a href="#about" v-smooth-scroll>About</a>
            </li>
            <li :class="Toggle ? 'nav__link__mobile' : 'nav__link'">
              <a href="#skills" v-smooth-scroll>Skills</a>
            </li>
            <li :class="Toggle ? 'nav__link__mobile' : 'nav__link'">
              <a href="#work" v-smooth-scroll>Work</a>
            </li>
            <li :class="Toggle ? 'nav__link__mobile' : 'nav__link'">
              <a href="#contact" v-smooth-scroll>Contact</a>
            </li>
          </ul>
        </div>
      </nav>
    </transition>
    <div class="nav__toggle" @click="navToggle">
      <i :class="Toggle ? ' far fa-minus-square nav__active' : ''"></i>
      <i :class="Toggle ? '' : 'far fa-caret-square-down nav__active '"></i>
    </div>
  </header>
</template>

<script>
export default {
  name: "NavBar",
  data() {
    return {
      Toggle: false,
      desktop: true,
    };
  },
  created() {
    window.addEventListener("resize", this.checkScreen);
    this.checkScreen();
  },
  methods: {
    checkScreen() {
      if (window.innerWidth < 600) {
        this.desktop = false;
      } else {
        this.desktop = true;
        this.Toggle = false;
      }
    },
    navToggle() {
      this.Toggle = !this.Toggle;
      this.desktop = !this.desktop;
      console.log(this.Toggle);
    },
    scrollToMyEl() {
      const myEl = this.$refs.myEl || this.$el || document.getElementById();

      this.$smoothScroll({
        scrollTo: myEl, // scrollTo is also allowed to be number
        hash: "#sampleHash", // required if updateHistory is true
      });
    },
  },
};
</script>

<style scoped>
li,
a,
button {
  font-weight: 500;
  font-size: 16px;
  text-decoration: none;
}
header {
  display: flex;
  position: fixed;
  justify-content: flex-end;
  align-items: center;
  width: 100%;
  padding: 15px 10%;
  border-bottom: 1px solid rgba(64, 112, 244, 0.8);
  z-index: 1000;
  background-color: #fff;
}
.logo {
  cursor: pointer;
  margin-right: auto;
  opacity: 1;
  transition: opacity 0.3s ease 0s;
}
.nav__list {
  list-style: none;
}
.nav__link {
  display: inline-block;
  padding: 0px 20px;
}
.nav__link a {
  transition: all 0.3s ease 0s;
}
.nav__link a:hover {
  color: rgba(66, 62, 62, 0.712);
}
.nav__link:hover {
  position: relative;
}
.nav__link {
  position: relative;
}
.far {
  display: none;
}
.nav__link:hover::after {
  position: absolute;
  content: "";
  width: 100%;
  height: 0.18rem;
  left: 0;
  top: 2rem;
  background-color: rgba(64, 112, 244, 0.8);
}
.link {
  transition: all 0.3s ease 0s;
}
.link:hover {
  color: rgba(66, 62, 62, 0.712);
}
button:hover {
  background-color: rgba(64, 112, 244, 0.8);
}

.active::after {
  position: absolute;
  content: "";
  width: 100%;
  height: 0.18rem;
  left: 0;
  top: 2rem;
  background-color: #4070f4;
}
@media only screen and (max-width: 600px) {
  .nav__active {
    display: block;
    position: fixed;
    z-index: 50000;
    cursor: pointer;
    margin-left: auto;
    top: 0;
    right: 10px;
  }
  .appear-enter-active {
    opacity: 1;
    transition: opacity 0.8s ease-in;
  }

  .appear-enter-from {
    opacity: 0;
  }
  .fade-enter-active,
  .fade-leave-active {
    /* top: 0; */
    transform: translateY(0);
    opacity: 1;
    transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  }

  .fade-enter-from,
  .fade-leave-to {
    transform: translateY(-1000px);
    opacity: 0;
  }
  .nav__menu {
    display: block;
  }
  .far {
    font-size: 2rem;
    color: #4070f4;
  }
  .nav__link {
    display: none;
  }
  .nav__list__mobile {
    text-align: center;
    height: 50vh;
    overflow-y: auto;
    width: 100vw;
    display: flex;
    position: relative;
    flex-direction: column;
    top: -15px;
    justify-content: space-evenly;
    left: 0px;
    /* background-color: rgba(64, 112, 244, 0.8); */
    z-index: 1000;
    /* border-bottom: 1px solid rgba(64, 112, 244, 0.8); */
  }
  .nav__link__mobile {
    /* margin-top: auto; */
  }

  header {
    /* background-color: rgba(64, 112, 244, 0.8); */

    justify-content: center;
  }
}
</style>
