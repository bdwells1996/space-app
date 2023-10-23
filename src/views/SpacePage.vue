

<template>
    <div class="space-page">
      <header class="space-page__header">
        <h1 class="space-page__header__title">
            Space
        </h1>
        <p class="space-page__header__text">Lorem ipsum dolor sit amet consectetur. Nulla tortor sit venenatis viverra. Mattis vivamus in eget proin lacus eget morbi sed. Nulla imperdiet venenatis aliquam sed consectetur nec. Cursus dignissim et mattis suspendisse ullamcorper vitae ligula. In venenatis mi molestie cursus consequat ullamcorper molestie. Et donec odio nisi fames maecenas lobortis. Morbi nunc mauris et nascetur vulputate.</p>
        <img src="/src/assets/images/space-example.jpg" alt="space background" class="space-page__header__bg" />
      </header>

    <div class="museum-highlight">

        <MuseumHighlight v-for="highlight in highlights" :highlight="highlight" :key="highlight.id">
          <template v-slot:icon>
            <p class="museum-highlight__inner__icon__text">Space</p>
            <img class="museum-highlight__inner__icon__image" :src="spaceIcon" alt="space page icon" />
          </template>

          <template v-slot:additional-actions>
            <a v-if="highlight.quiz" :href="highlight.quiz" class="museum-highlight__inner__actions__button">Take the quiz</a>
          </template>
        </MuseumHighlight>

    </div>

    </div>
</template>

<script>

import MuseumHighlight from '../components/MuseumHighlight.vue';

export default {
    name: 'SpacePage',
    components: {
        MuseumHighlight,
    },
    mixins: [
    ],
    props: {

    },
    data() {
        return {
            spaceIcon: 'src/assets/space-icon.png',
            spaceHighlights: [
                {
                    date: '2020-04-20 12:20:00',
                    description: 'Asteroids are minor planets, especially of the inner Solar System. Larger asteroids have also been called planetoids.',
                    id: 1,
                    image: '',
                    name: 'Asteroids',
                },
                {
                    date: '2020-05-20 15:50:00',
                    description: 'A comet is an icy, small Solar System body that, when passing close to the Sun, warms and begins to release gases, a process called outgassing.',
                    id: 9,
                    image: '',
                    name: 'Comets',
                },
                {
                    date: '2020-05-01 9:22:00',
                    description: 'The term planet is ancient, with ties to history, astrology, science, mythology, and religion.',
                    id: 7,
                    image: '',
                    name: 'Planets',
                    news: {
                        date: '2020-08-18 18:00:00',
                        title: 'Attend our talk about Jupiter with Dr. Hogarth',
                    },
                    quiz: 'https://planetquiz.space',
                },
                {
                    date: '2020-07-05 4:10:00',
                    description: 'A meteor shower is a celestial event in which a number of meteors are observed to radiate, or originate, from one point in the night sky.',
                    id: 12,
                    image: '',
                    name: 'Meteor showers',
                    news: {
                        title: 'The Lyrids will peak at on April 21-22 2021, at night',
                    },
                },
            ],
            spacePartners: {
                observatory: {
                    createdAt: '2020-06-01 11:45:00',
                    info: 'The Mauna Kea Observatories (MKO) are a number of independent astronomical research facilities and large telescope observatories that are located at the summit of Mauna Kea on the Big Island of Hawaiʻi, United States.',
                    image: '',
                    name: 'Mauna Kea Observatories',
                },
            },
        };
    },
    computed: {
      mapPartnerData() {
        const spacePartnerKeys = Object.keys(this.spacePartners);
        return spacePartnerKeys.map((key) => {
          const partner = this.spacePartners[key];
          return {

            // Defines schema, default values for partner data 

            id: new Date(partner.createdAt).getTime(),
            date: partner.createdAt,
            description: partner.info,
            image: partner.image,
            name: partner.name,
            news: null,
            quiz: null,
            isPartner: true,
          };
        });
      },
        highlights() {
            return this.spaceHighlights
            .concat(this.mapPartnerData)
            .sort(this.sortByDate);
        }
    },
    methods: {
      sortByDate(a, b) {
      return new Date(b.date) - new Date(a.date);
    },
    },
    created() {

    },
};
</script>

<style lang="scss" scoped>
.space-page {
  &__header {
    position: relative;
    height: 380px;
    border-radius: 0 0 12px 12px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 0 43px;
    overflow: hidden;
    box-shadow: 0px 3px 8px 0px rgba(0, 0, 0, 0.15);

      &__title {
      color: #fff;
      font-size: 56px;
      font-weight: 600;
      margin: 0 0 20px;
      }

      &__text{
        font-size: 18px;
        color: #fff;
        max-width: 1060px;
      }

  &__bg{
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
  }
  }
}

.museum-highlight {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    column-gap: 40px;
    row-gap: 40px;
    padding: 0 42px;
    margin-top: 40px;

}

.museum-highlight__inner__actions__button{
        background: #AAAACE;
        border: none;
        border-radius: 3px;
        font-size: 16px;
        font-family: 'Montserrat', sans-serif;
        appearance: none;
        margin-left: 20px;
        padding: 10px 26px;
        cursor: pointer;
        transition: background 200ms ease;
        color: #000;
        text-decoration: none;
        text-align: center;

        &:hover{
            background: #8989b7;
        }
    }


</style>
