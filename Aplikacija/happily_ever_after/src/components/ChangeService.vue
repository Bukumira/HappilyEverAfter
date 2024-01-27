<template>
  <div class="register-page">
    <h1>Izmeni uslugu</h1>
    <form @submit.prevent="saveData">
      <div class="form-columns">
        <div class="form-column">
      <div class="form-group">
        <label for="naziv">Naziv:</label>
        <input placeholder="Naziv" type="text" name="naziv" v-model="service.name" required />
      </div>
      <div class="form-group">
        <label for="naziv">Tip(Muzika, Dekoracija, Fotografisanje...):</label>
        <input placeholder="Tip" type="text" name="tip" v-model="service.type" required />
      </div>
      <div class="form-group">
        <label for="naziv">Lokacija:</label>
        <input
          placeholder="Lokacija"
          type="text"
          name="lokacija"
          v-model="service.location"
          required
        />
      </div>
      <div class="form-group">
        <label for="naziv">Opis:</label>
            <input placeholder="Opis" type="text" name="opis" v-model="service.description" required />
          </div>
      <div class="form-group">
        <label for="naziv">Cena:</label>
        <input placeholder="Cena" type="number" name="cena" v-model="service.price" />
        </div>
        <div class="form-group">
          <label for="naziv">Kolicina:</label>
        <input placeholder="Unit" type="text" name="unit" v-model="service.unit" />
      </div>
      <div class="form-group">
        <label for="naziv">Link:</label>
        <input placeholder="Link" type="text" name="link" v-model="service.link" required />
      </div>
      <div class="form-group">
        <label for="naziv">Telefon:</label>
        <input
          placeholder="Telefon"
          type="text"
          name="telefon"
          v-model="service.phoneNumber"
          required
        />
      </div>
    </div>
    <div class="form-column">
      <div class="form-group">
        <label for="naziv">Slika:</label>
        <input placeholder="Slika" type="text" name="slika" v-model="service.img" />
      </div>
      <div class="form-group">
        <label for="naziv">Rezervisani datumi:</label>
        <input placeholder="Datumi" type="date" name="datumi" v-model="service.reserved_dates" />
      </div>
      <div class="form-group">
        <label for="naziv">Boja:</label>
        <input placeholder="Boja" type="text" name="boja" v-model="service.color" />
      </div>
      <div class="form-group">
        <label for="naziv">Velicina:</label>
        <input placeholder="Velicina" type="text" name="velicina" v-model="service.size" />
      </div>
      <div class="form-group">
        <label for="naziv">Podusluga(Nokti, Sminka, Pozivnice...):</label>
        <input
          placeholder="Subservice"
          type="text"
          name="subservice"
          v-model="service.subservice"
        />
      </div>
      <div class="form-group">
        <label for="naziv">Meni:</label>
        <input placeholder="Meni" type="text" name="meni" v-model="service.menus" />
      </div>
      <div class="form-group">
        <label for="naziv">Broj gostiju:</label>
        <input
          placeholder="Broj gostiju"
          type="number"
          name="broj_gostiju"
          v-model="service.max_guest_number"
        />
      </div>
      <div class="form-group">
        <label for="naziv">Prodavnica:</label>
        <input placeholder="Prodavnica" type="text" name="prodavnica" v-model="service.store" />
      </div>
    </div>
    </div>

      <div class="form-group">
        <div class="left">
          <router-link class="link" to="/servicesPage">Nazad</router-link>
        </div>
        <div class="button-group">
        <button type="submit">Izmeni</button>
      </div>
      </div>
    </form>
  </div>
</template>
<script>
import axios from 'axios'

export default {
  name: 'ChangeService',
  data() {
    return {
      result: {},
      service: {
        id: '',
        name: '',
        type: '',
        location: '',
        description: '',
        price: '',
        unit: '',
        link: '',
        phoneNumber: '',
        img: '',
        reserved_dates: [],
        color: '',
        size: '',
        menus: [],
        subservice: '',
        max_guest_number: '',
        store: ''
      }
    }
  },
  created() {
    this.getServiceData()
  },
  mounted() {
    console.log('mounted() called...')
  },
  methods: {
    async getServiceData() {
      try {
        const serviceId = this.$route.params.id
        const response = await axios.get(
          'http://localhost:3000/service/get_service_by_id/' + serviceId
        )
        this.service = response.data
      } catch (error) {
        console.error(error)
      }
    },
    handleImageUpload(event) {
      const file = event.target.files[0]
      this.service.img = file
    },
    saveData() {
      axios
        .put('http://localhost:3000/service/' + this.service._id, this.service)
        .then((response) => {
          // Handle the successful response if needed
          console.log('Service updated:', response.data)
          this.$router.push('/servicesPage')
        })
        .catch((error) => {
          // Handle the error if needed
          console.error(error)
        })
    }
  }
}
</script>

<style scoped>
.register-page {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: rgba(150, 150, 150, 0.5);
  width: 90%;
  max-width: 800px;
  height: 100vh;
  padding: 10%;
  border-radius: 20px;

}

h1 {
  font-size: 35px;
  color: white;
  font-weight: 600;
  margin-bottom: 3vh;
  margin-top: 3vh;
}

p {
  font-size: 20px;
  color: white;
}

.form-columns {
  display: flex;
  justify-content: space-between;
}

.form-column {
  flex: 1;
  margin-right: 20px;
}
.button-group {
  display: flex;
  justify-content: flex-end;
  margin-bottom: 20px; 
}
.form-group {
  margin-bottom: 0px;
}

input {
  border-radius: 10px;
  border: 0;
  height: 40px;
  width: 100%;
  color: white;
  font-size: 16px;
  background: rgba(255, 255, 255, 0.3);
  padding-left: 20px;
  padding-right: 20px;
  transition: all 0.5s ease;
}

input::placeholder {
  color: white;
}

label {
  color: aliceblue;
  font: italic;
}

button {
  background: var(--light-pink);
  border: 0;
  color: var(--font-dark);
  width: 50%;
  border-radius: 10px;
  height: 50px;
  font-size: 16px;
  font-weight: bold;
  margin-bottom: 3vh;
}

.link {
  color: white;
  justify-self: left;
  padding: 5px;
  font-size: 16px;
}


.link:hover {
  background-color: var(--white-pink);
  color: var(--font-dark);
  border: 0;
  border-radius: 10px;
}

.left,
.right {
  width: 50%;
  display: flex;
}

.left {
  justify-content: flex-start;
}

.right {
  justify-content: flex-end;
}

input:hover {
  border: 1px solid white;
  background: rgba(255, 255, 255, 0.08);
}


@media (max-width: 700px) {
  button,
  input,
  .link,
  p {
    font-size: 14px;
  }

  h1 {
    font-size: 24px;
  }
}

@media (width<1000px){
    .register-page{
       padding:18% !important;
    }
}
</style>
