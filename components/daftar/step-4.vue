<template>
  <div>
    <div class="body-2 primary__dark--text">
      <v-icon small>help</v-icon>
      Kamu bisa menambahkan hingga 5 prestasi terbaikmu
    </div>
    <v-card v-for="(achievement, index) in model.achievements" :key="index" class="fls-form-group elevation-3 my-2">
      <v-card-title>
        <v-spacer></v-spacer>
        <v-btn color="error" small icon @click="removeFormAchievement(index)"><v-icon small>delete</v-icon></v-btn>
      </v-card-title>
      <v-card-text>
        <v-text-field
          v-model="achievement.name"
          label="Prestasi"
          data-vv-as="Prestasi"
          :error-messages="errors.collect('name' + index)"
          v-validate="'required'"
          :data-vv-name="'name' + index"
          required
        ></v-text-field>
        <v-select
          :items="levelItems"
          v-model="achievement.level"
          data-vv-as="Tingkat"
          :error-messages="errors.collect('level' + index)"
          v-validate="'required'"
          :data-vv-name="'level' + index"
          label="Tingkat"
        ></v-select>
        <v-select
          :items="rankItems"
          v-model="achievement.rank"
          data-vv-as="Peringkat"
          :error-messages="errors.collect('rank' + index)"
          v-validate="'required'"
          :data-vv-name="'rank' + index"
          label="Peringkat"
        ></v-select>
        <v-select
          :items="yearItems"
          v-model="achievement.year"
          label="Tahun"
          data-vv-as="Tahun"
          :error-messages="errors.collect('year' + index)"
          v-validate="'required'"
          :data-vv-name="'year' + index"
          required
        ></v-select>
      </v-card-text>

    </v-card>
    <v-btn v-if="this.model.achievements.length < 5" block @click="newFormAchievement()" round color="info">Tambah</v-btn>
  </div>
</template>

<script>
export default {
  data () {
    return {
      model: {
        achievements: []
      },
      rankItems: [
        'Juara 1',
        'Juara 2',
        'Juara 3',
        'Peserta',
      ],
      levelItems: [
        'Internasional',
        'Nasional',
        'Daerah',
        'Universitas',
        'Sekolah'
      ],
      yearItems: [
        2018,
        2017,
        2016,
        2015,
        2014,
        2013
      ]
    }
  },
  methods: {
    newFormAchievement () {
      if (this.model.achievements.length < 5) {
        this.model.achievements.push({
          name: '',
          year: '',
          level: '',
          rank: ''
        })
      }
    },
    removeFormAchievement (index) {
      this.model.achievements.splice(index, 1)
    },
    validate () {
      return new Promise((resolve, reject) => {
        this.$validator.validateAll().then((valid) => {
          let errors = this.errors.collect()
          resolve({ valid: valid, model: this.model, error: errors[Object.keys(errors)[0]]});
        });
      })
    }
  }
}
</script>
