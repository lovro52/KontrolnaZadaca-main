<template>
	<v-container fill-height fluid class="background">
		<v-row>
			<v-col cols="12">
				<v-card class="pa-3" outlined width="600px">
					<v-card-title>Register</v-card-title>
					<v-card-text>
						<v-form v-model="valid">
							<v-text-field v-model="firstName" dense label="Ime" clearble type="text"
								outlined></v-text-field>
							<v-text-field v-model="lastName" dense label="Prezime" clearble type="text"
								outlined></v-text-field>
							<v-text-field v-model="brojDolazaka" dense label="Broj Dolazaka(maksimalno 15)" clearble
								type="text" :rules="[rules.required, rules.max15]" outlined></v-text-field>
							<v-text-field v-model="rezultatPrvogKolokvija" dense
								label="Rezultat prvog kolokvija(maksimalno 40 bodova)" clearble type="text"
								:rules="[rules.required, rules.max40]" outlined></v-text-field>
							<v-text-field v-model="rezultatDrugogKolokvija" dense
								label="Rezultat drugog kolokvija(maksimalno 40 bodova)" clearble type="text"
								:rules="[rules.required, rules.max40]" outlined></v-text-field>
							<v-text-field v-model="kontinuiranoPracenje" dense
								label="Kontinuirano pracenje(maksimalno 20 bodova)" clearble type="text"
								:rules="[rules.required, rules.max20]" outlined></v-text-field>
						</v-form>
					</v-card-text>
					<v-card-actions>
						<v-btn color="black" class="white--text" elevation="0" @click="obrisiSveUnesenePodatke">
							BRISI PODATKE
						</v-btn>
						<v-spacer></v-spacer>
						<v-btn class="btn-right-margin" @click="ocistiFormu" color="red darken-3" outlined>
							CLEAR
						</v-btn>
						<v-btn :disabled="isButtonDisabled" outlined @click="registerUser">
							OK
						</v-btn>
					</v-card-actions>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
export default {
	name: "prvi-zadatak",
	data() {
		return {
			isButtonDisabled: false,
			valid: true,
			firstName: null,
			lastName: null,
			brojDolazaka: null,
			rezultatPrvogKolokvija: null,
			rezultatDrugogKolokvija: null,
			kontinuiranoPracenje: null,
			rules: {
				required: (value) => !!value || "Required.",
				min: (v) => v?.length >= 6 || "Min 6 characters",
				max15: (v) => v <= 15 || "Maksimalno 15 bodova",
				max20: (v) => v <= 20 || "Maksimalno 20 bodova",
				max40: (v) => v <= 40 || "Maksimalno 40 bodova",

			},
		};
	},
	watch: {
		valid: function (isValid) {
			this.isButtonDisabled = isValid != true;
		}
	},
	methods: {
		ocistiFormu() {
			this.firstName = null;
			this.lastName = null;
			this.brojDolazaka = null;
			this.rezultatPrvogKolokvija = null;
			this.rezultatDrugogKolokvija = null;
			this.kontinuiranoPracenje = null;
		},
		dodajStudenta() {
			let noviStudent = {
				//Dodaj propertyje
				ime: this.firstName,
				prezime: this.lastName,
				brojDolazaka: this.brojDolazaka,
				prviKolokvij: this.rezultatPrvogKolokvija,
				drugiKolokvij: this.rezultatDrugogKolokvija,
				kontinuiranoPracenje: this.kontinuiranoPracenje,
			};
			//ovo ne diraj
			let studenti = JSON.parse(localStorage.getItem("studenti"));
			if (!studenti) {
				studenti = [];
			}
			studenti.push(noviStudent);
			localStorage.setItem("studenti", JSON.stringify(studenti));
		},
		obrisiSveUnesenePodatke() {
			localStorage.clear();
		},
	},
};
</script>
