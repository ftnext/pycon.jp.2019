<template lang="pug">
.schedule-table(:class="{'pl-4': $vuetify.breakpoint.mdAndUp}")
    // header
    row(v-if="$vuetify.breakpoint.smAndUp")
        v-layout.wrap
            v-flex.xs12.sm12.md2.text-md-center(v-for="(room, idx) in rooms" :key="idx")
                p.body-2.font-weight-bold {{ $t('rooms.' + roomsMaster[room]) }}
    row(time="09:30")
        v-layout.wrap
            v-flex.pa-2.text-md-center.text-xs-center.subheading {{ $t("timetable.open") }}
    row(time="10:00")
        v-layout.wrap
            v-flex.xs12.sm12.md2.pa-2.blueGrey2
                simple-card(:roomIds="[1006]") {{ $t("timetable.keynote") }}
            v-flex.xs12.sm12.md2(v-for="(_, idx) in 5" :key="idx")
    row(time="11:15")
        v-layout.wrap
            v-flex.xs12.sm12.md2.pa-2(v-for="(room, idx) in rooms" :key="idx" :class="idx % 2 == 0 ? 'blueGrey2' : ''")
                card(v-if="matchSession(room, 1)" :session="matchSession(room, 1)")
    row(time="12:00")
        v-layout.wrap
            v-flex.xs12.sm12.md12.pa-2.blueGrey2
                simple-card(:roomIds="[1006, 1001, 1002, 1003, 1004, 1005]") {{ $t("timetable.lunch") }}
    row(time="13:30")
        v-layout.wrap
            v-flex.xs12.sm12.md2.pa-2(v-for="(room, idx) in rooms" :key="idx" :class="idx % 2 == 0 ? 'blueGrey2' : ''")
                card(v-if="matchSession(room, 2)" :session="matchSession(room, 2)")
    row(time="14:15")
        v-layout.wrap
            v-flex.xs12.sm12.md2.pa-2(v-for="(room, idx) in rooms" :key="idx" :class="idx % 2 == 0 ? 'blueGrey2' : ''")
                card(v-if="matchSession(room, 3)" :session="matchSession(room, 3)")
    row(time="14:45")
        v-layout.wrap
            v-flex.xs12.sm12.md2.pa-2.blueGrey2
                simple-card(:roomIds="[1006]") {{ $t("timetable.poster") }} / {{ $t("timetable.coffee") }}
            v-flex.xs12.sm12.md2(v-for="(_, idx) in 5" :key="idx")
    row(time="15:45")
        v-layout.wrap
            v-flex.xs12.sm12.md2.pa-2(v-for="(room, idx) in rooms" :key="idx" :class="idx % 2 == 0 ? 'blueGrey2' : ''")
                card(v-if="matchSession(room, 4)" :session="matchSession(room, 4)")
    row(time="16:15")
        v-layout.wrap
            v-flex.xs12.sm12.md2.pa-2(v-for="(room, idx) in rooms" :key="idx" :class="idx % 2 == 0 ? 'blueGrey2' : ''")
                card(v-if="matchSession(room, 5)" :session="matchSession(room, 5)")
    row(time="16:45")
        v-layout
            v-flex.xs12.sm12.md2.pa-2.blueGrey2
                simple-card(:roomIds="[1006]") {{ $t("timetable.lt") }}
            v-flex.md2(v-for="(_, idx) in 5" :key="idx")
    row(time="17:20")
        v-layout
            v-flex.xs12.sm12.md2.pa-2.blueGrey2
                simple-card(:roomIds="[1006]") {{ $t("timetable.smlt") }}
            v-flex.md2(v-for="(_, idx) in 5" :key="idx")
    row(time="17:40")
        v-layout
            v-flex.xs12.sm12.md2.pa-2.blueGrey2
                simple-card(:roomIds="[1006]") {{ $t("timetable.photo2") }}
            v-flex.md2(v-for="(_, idx) in 5" :key="idx")
    row(time="17:50" :no-border="true")
        v-layout
            v-flex.pa-2.text-md-center.text-xs-center.subheading {{ $t("timetable.closing") }}
    row(time="18:20")

</template>

<style lang="sass" scoped>
@media only screen and (max-width: 1200px)
    .flex
        background-color: white !important
</style>


<script>
import Vue from 'vue'

import Card from "@/components/pages/schedule/Card"
import SimpleCard from "@/components/pages/schedule/SimpleCard"
import Row from "@/components/pages/schedule/Row"
import { roomsMaster } from "@/plugins/constants"

export default Vue.extend({
    name: "time-table",
    props: ['sessions'],
    components: {
        "card": Card, "row": Row, "simple-card": SimpleCard
    },
    data()  {
        return {
            rooms: [1006, 1001, 1002, 1003, 1004, 1005],
            roomsMaster: roomsMaster
        }
    },
    created() {
    },
    methods: {
        matchSession(roomId, no) {
            const matchs = this.sessions.filter(s => s.room_id == roomId && s.no == no)
            return matchs.length > 0 ? matchs[0] : null
        }
    }
})
</script>