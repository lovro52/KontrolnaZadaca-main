<template>
	<!-- Ne diraj ovu komponentu -->
	<v-container>
		<DefinicijaZadatka>
			<v-row class="text-center">
				<v-col cols="12">
					<v-card class="card-border overflow" :width="width" :height="height" outlined>
						<v-card-text>
							<v-card outlined>
								<div v-show="viewName == 'prvi-zadatak'">
									<v-img src="@/assets/zad1-1.png"></v-img>
									<v-img src="@/assets/zad1-2.png"></v-img>
									<v-img src="@/assets/zad1-3.png"></v-img>
								</div>
								<div v-show="viewName == 'drugi-zadatak'">
									<v-img src="@/assets/zad2-1.png"></v-img>
									<v-img src="@/assets/zad2-2.png"></v-img>
									<v-img src="@/assets/zad2-3.png"></v-img>
								</div>
							</v-card>
						</v-card-text>
					</v-card>
				</v-col>
			</v-row>
		</DefinicijaZadatka>
	</v-container>
</template>

<script>
import DefinicijaZadatka from "./DefinicijaZadatka.vue"
export default {
	name: "DefinicijaZadatka",
	props: ["viewName", "height", "width"],
	data() {
		return {};
	},
	components: {
		DefinicijaZadatka
	}
};
</script>
<style>
.overflow {
	height: 100%;
	overflow-y: scroll;
}
</style>
