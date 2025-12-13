<template>
    <b-card class="threat-card">
        <b-card-text>
            <b-row>
                <b-col>
                    <a
                        href="javascript:void(0)"
                        @click="threatSelected()"
                        v-if="!!numberResolved"
                    >
                        #{{ numberResolved }} {{ titleResolved || 'Unknown Threat' }}
                    </a>
                    <a
                        href="javascript:void(0)"
                        @click="threatSelected()"
                        v-else
                    >
                        {{ titleResolved || 'Unknown Threat' }}
                    </a>
                </b-col>
            </b-row>

            <b-row v-if="modelTypeResolved !== 'EOP' && typeResolved">
                <b-col>
                    {{ typeResolved }}
                </b-col>
            </b-row>

            <b-row v-if="modelTypeResolved === 'EOP'">
                <b-col>
                    <b-row>
                        <b-col>
                            {{ cardsuit }}
                        </b-col>
                    </b-row>
                    <b-row>
                        <b-col>
                            {{ cardnumber }}
                        </b-col>
                    </b-row>
                </b-col>
            </b-row>
            <b-row>
                <b-col>
                    <font-awesome-icon
                        icon="check"
                        class="threat-icon gray-icon"
                        :title="statusResolved"
                        v-if="statusResolved === 'NotApplicable'"
                    />
                    <font-awesome-icon
                        icon="check"
                        class="threat-icon green-icon"
                        :title="statusResolved"
                        v-if="statusResolved === 'Mitigated'"
                    />
                    <font-awesome-icon
                        icon="exclamation-triangle"
                        class="threat-icon red-icon"
                        :title="statusResolved"
                        v-if="statusResolved === 'Open'"
                    />

                    <font-awesome-icon
                        icon="circle"
                        class="threat-icon darkred-icon"
                        :title="severityResolved"
                        v-if="severityResolved === 'Critical'"
                    />
                    <font-awesome-icon
                        icon="circle"
                        class="threat-icon red-icon"
                        :title="severityResolved"
                        v-if="severityResolved === 'High'"
                    />
                    <font-awesome-icon
                        icon="circle"
                        class="threat-icon orange-icon"
                        :title="severityResolved"
                        v-if="severityResolved === 'Medium'"
                    />
                    <font-awesome-icon
                        icon="circle"
                        class="threat-icon yellow-icon"
                        :title="severityResolved"
                        v-if="severityResolved === 'Low'"
                    />
                    <font-awesome-icon
                        icon="circle"
                        class="threat-icon gray-icon"
                        :title="severityResolved"
                        v-if="severityResolved === 'TBD'"
                    />
                </b-col>
                <b-col align-h="end">
                    <b-badge v-if="!!modelTypeResolved">
                        {{ modelTypeResolved }}
                    </b-badge>
                </b-col>
            </b-row>
        </b-card-text>
    </b-card>
</template>

<style lang="scss" scoped>
.threat-card {
    font-size: 14px;
}

.threat-title {
    margin-bottom: 5px;
}

.threat-icon {
    margin: 2px;
}

.green-icon {
    color: $green;
}

.darkred-icon {
    color: $firebrick;
}

.red-icon {
    color: $red;
}

.orange-icon {
    color: $darkorange;
}

.yellow-icon {
    color: $yellow;
}

.gray-icon {
    color: $gray;
}

</style>
<script>
export default {
    name: 'TdGraphThreats',
    props: {
        // Nuevo modelo
        threat: {
            type: Object,
            required: false,
            default: null
        },

        // Modelo antiguo (tests)
        id: { type: String },
        status: { type: String },
        severity: { type: String },
        description: { type: String },
        title: { type: String },
        type: { type: String },
        mitigation: { type: String },
        modelType: { type: String },
        number: { type: Number },
        cardSuit: { type: String },
        cardNumber: { type: String }
    },

    computed: {
        threatData() {
            return this.threat || {
                id: this.id ?? '',
                status: this.status ?? '',
                severity: this.severity ?? '',
                description: this.description ?? '',
                title: this.title ?? '',
                type: this.type ?? '',
                mitigation: this.mitigation ?? '',
                modelType: this.modelType ?? '',
                number: this.number ?? null,
                cardSuit: this.cardSuit ?? '',
                cardNumber: this.cardNumber ?? ''
            };
        },

        idResolved() { return this.threatData.id; },
        statusResolved() { return this.threatData.status; },
        severityResolved() { return this.threatData.severity; },
        descriptionResolved() { return this.threatData.description; },
        titleResolved() { return this.threatData.title; },
        typeResolved() { return this.threatData.type; },
        mitigationResolved() { return this.threatData.mitigation; },
        modelTypeResolved() { return this.threatData.modelType; },
        numberResolved() { return this.threatData.number; },
        cardsuit() { return this.threatData.cardSuit; },
        cardnumber() { return this.threatData.cardNumber; }
    },

    methods: {
        threatSelected() {
            this.$emit('threatSelected', this.idResolved, 'old');
        }
    }
};
</script>