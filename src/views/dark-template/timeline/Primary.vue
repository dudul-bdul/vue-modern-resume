<template>
  <v-card
    color="grey lighten-4"
    light
  >
    <v-card-text>
      <content-section
        id="timeline"
        :title="detailed ? 'My Life in a Nutshell' : 'My Experiences'"
      >
        <template slot="actions">
          <div>
            <v-switch
              v-model="detailed"
              :label="detailed ? 'Detailed' : 'Summary'"
            />
          </div>
        </template>

        <v-timeline
          dense
        >
          <v-timeline-item
            v-for="(item, i) in orderedItems"
            :key="i"
            :icon="item.icon || ''"
            :class="{transparent: item.transparent}"
            large
          >
            <template
              v-if="item.iconImage"
              v-slot:icon
            >
              <v-avatar>
                <img
                  :src="publicPath(item.iconImage)"
                >
              </v-avatar>
            </template>
            <template v-slot:opposite />
            <v-layout>
              <v-flex
                v-if="$vuetify.breakpoint.smAndUp"
                md1
                sm2
                align-self-center
              >
                <span>{{ item.year }}</span>
              </v-flex>
              <v-flex
                md11
                sm10
                xs12
              >
                <v-card class="elevation-1">
                  <v-card-title class="pb-0">
                    <div>
                      <p v-if="$vuetify.breakpoint.xsOnly">
                        {{ item.year }}
                      </p>
                      <h3>{{ item.title }}</h3>
                    </div>
                  </v-card-title>
                  <v-card-text>
                    <v-layout wrap>
                      <v-flex
                        :md7="!!item.image"
                        :md12="!item.image"
                        xs12
                      >
                        <div class="mr-1">
                          <span
                            v-if="item.text"
                            class="pre"
                          >{{ item.text }}</span>
                          <!-- eslint-disable vue/no-v-html -->
                          <div
                            v-else-if="item.html"
                            v-html="item.html"
                          />
                          <!-- eslint-enable vue/no-v-html -->
                        </div>
                      </v-flex>
                      <v-flex
                        v-if="item.image"
                        md5
                        xs12
                      >
                        <div
                          class="mt-2"
                        >
                          <v-carousel
                            v-if="Array.isArray(item.image)"
                            :show-arrows="false"
                            :height="325"
                          >
                            <v-carousel-item
                              v-for="(citem,ci) in item.image"
                              :key="ci"
                              :src="publicPath(citem)"
                            />
                          </v-carousel>
                          <v-img
                            v-else
                            :max-height="item.imageHeight ? item.imageHeight : ''"
                            :src="publicPath(item.image)"
                          />
                        </div>
                      </v-flex>
                    </v-layout>
                  </v-card-text>
                </v-card>
              </v-flex>
            </v-layout>
          </v-timeline-item>
        </v-timeline>
      </content-section>
    </v-card-text>
  </v-card>
</template>

<script>
import ContentSection from '@/views/dark-template/content/Section'
export default {
  name      : 'Timeline',
  components: { ContentSection },
  data      : () => ({
    detailed: true,
    items   : [
      {
        detailed   : true,
        transparent: true,
        year       : '1991',
        title      : 'Born on July, 1991',
        html       : 'With a chance of %0.00000000000512.<br>I\'m completely aware of value of the life!',
        icon       : 'mdi-cake-variant',
      },
      {
        detailed   : true,
        transparent: true,
        year       : '2003',
        title      : 'Touched a Mouse',
        html       : 'ME: "Woooow!"<br><i>... Of course got slapped later!</i>',
        icon       : 'mdi-mouse-variant',
      },
      

      
      
      {
        detailed   : true,
        transparent: true,
        year       : '2018',
        title      : 'A Turning Point',
        html       : `
          <p>
          It looks like that 2018 is missing from my CV isn't it? <strong>NOT AT ALL!</strong>
          </p>
          <p>
          This awesome year was a turning point in my life. I found out the reason why my businesses are not growing; what I'm doing wrong; what I've supposed to do and plenty of other thoughts.
          </p>
          <p>
          Technically, I got familiar with and tried to be best (not yet of course!) at the following technologies:
          <ul>
          <li>git</li>
          <li>Laravel</li>
          <li>Vue.js</li>
          <li>Arduino</li>
          <li>Ubuntu</li>
          <li>TTD and CI/CD</li>
          <li>Development best practices</li>
          <li>And more ...</li>
          </ul>
          </p>
          <p>
          So please don't underestimate this card by its height in pixels. It's worth a lot to me.
          </p>

        `,
        icon: 'mdi-cake-variant',
      },
      {
        year : '2019',
        title: 'Open Sourced Telegram Web Bridge',
        html : `
          <p>
              Current status: <span class="light-blue--text lighten-3">Open Sourced</span><br>Available on: <a target="_blank" href="https://github.com/AmirrezaNasiri/telegram-web-bridge">AmirrezaNasiri/telegram-web-bridge</a>
          </p>
          <p>
            Telegram Web Bridge is a bidirectional, web-based, proxy-like application which can act as a middleman for Telegram Bot API requests (from your actual application to Telegram) and Webhooks (from Telegram to your actual application).
          </p>
          <p>
            It was initially developed because of Telegram censorship in Iran and the need for it in a storage management software we've built. I decided to publish the codes so anyone with the same problem will be able to handle it.
          </p>
        `,
        image: 'img/timeline/telegram-web-bridge.png',
        icon : 'mdi-github-circle',
      },
      {
        year : '2019',
        title: 'Open Sourced USB Keystroke Injector',
        html : `
          <p>
            Current status: <span class="light-blue--text lighten-3">Open Sourced</span><br>Available on: <a target="_blank" href="https://github.com/AmirrezaNasiri/usb-keystroke-injector">AmirrezaNasiri/usb-keystroke-injector</a>
          </p>
          <p>
            An Arduino-based keyboard emulator which injects (i.e. types) a sequence of letters received via Bluetooth protocol or read from predefined SD card payloads. Demo GIF is available on the GitHub page.
          </p>
          <p>
            It was initially a university project, made at 2018 but I decided to extend it a little bit and publish it on my GitHub.
          </p>
        `,
        image: 'img/timeline/usb-keystroke-injector.png',
        icon : 'mdi-github-circle',
      },
      
      
      {
        year : '2019',
        title: 'Published Vue Registrar Package',
        html : `
          <p>
              Current status: <span class="light-blue--text lighten-3">Published</span><br>Available on: <a target="_blank" href="https://github.com/AmirrezaNasiri/vue-registrar">AmirrezaNasiri/vue-registrar</a>
          </p>
          <p>
            A Vue.js package that makes developers' code a lot cleaner and much more understandable. It's consisted of two features that:
            <ul>
                <li>Registers all your common and frequently used components globally and ends the need for importing them manually;</li>
                <li>Assembles all your vuex modules in a nested manner.</li>
            </ul>
          </p>
        `,
        image    : 'img/timeline/vue-registrar-demo.png',
        iconImage: 'img/timeline/vue-registrar-logo.png',
      },
      {
        year : 'So far ...',
        title: 'Written 340+ Unique Articles!',
        html : `I'm the guy who loves teaching! So far, I've written 340+ unique articles which most of them are computer-related. You can access them here:
 
`,
        icon: 'mdi-fountain-pen-tip',
      },
    ],
  }),
  computed: {
    orderedItems () {
      const items = [...this.items].reverse()
      if (this.detailed)
        return items
      return items.filter((item) => {
        return !item.detailed
      })
    },
  },
}
</script>

<style scoped>
.title {
  border-bottom: 2px #bfbfbf solid;
  line-height: 1.5 !important;
}
.pre {
  white-space: pre;
}
.transparent{
  opacity: 0.6;
}
</style>
