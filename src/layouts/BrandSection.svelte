<script>
  // json
  import offerData from "../json/offer-data.json";
  import universityData from "../json/university-data.json";
  // components
  import Offer from "../components/Offer.svelte";
  import UniversityHero from "../components/UniversityHero.svelte";
</script>

<Offer {offerData} />
<UniversityHero {universityData} />
