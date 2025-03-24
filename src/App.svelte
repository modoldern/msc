<script>
  // components
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import HomePage from "./pages/HomePage.svelte";
  import AvtorizaciisGadatsyvetileba from "./pages/Avtorizaciis-gadatsyvetileba.svelte";
  import Administracia from "./pages/Administracia.svelte";
  import Biblioteka from "./pages/Biblioteka.svelte";
  import BibliotekisSargeblobisTsesi from "./pages/Bibliotekis-sargeblobis-tsesi.svelte";
  import CharickhvisTsesi from "./pages/Charickhvis-tsesi.svelte";
  import EleqtronuliTsignebi from "./pages/Eleqtronuli-tsignebi.svelte";
  import GzamkvleviAplikantebs from "./pages/Gzamkvlevi-aplikantebs.svelte";
  import Diplomi from "./pages/Diplomi.svelte";
  import InformaciaSsmdaShshmPirebistvis from "./pages/Informacia-ssm-da-shshm-pirebistvis.svelte";
  import Katalogi from "./pages/Katalogi.svelte";
  import Kursdamtavrebulebi from "./pages/Kursdamtavrebulebi.svelte";
  import MaregulirebeliAqtebi from "./pages/Maregulirebeli-aqtebi.svelte";
  import MisiaKhedvaGhirebulebebi from "./pages/Misia-khedva-ghirebulebebi.svelte";
  import MsmenelisGzamkvlevi from "./pages/Msmenelis-gzamkvlevi.svelte";
  import Partniorebi from "./pages/Partniorebi.svelte";
  import ProfesiuliGanatlebisMastsavleblisprogramisGanmakhorcieleblisSamsakhurshiMighebisTsesi from "./pages/Profesiuli-ganatlebis-mastsavleblisprogramis-ganmakhorcieleblis-samsakhurshi-mighebis-tsesi.svelte";
  import ProfesiuliMastsavleblebi from "./pages/Profesiuli-mastsavleblebi.svelte";
  import ProfesiuliMastsavleblisGzamkvlevebi from "./pages/Profesiuli-mastsavleblis-gzamkvlevebi.svelte";
  import ProfesiuliMomzadebisprofesiuliGadamzadebisProgramebi from "./pages/Profesiuli-momzadebisprofesiuli-gadamzadebis-programebi.svelte";
  import ProfesiuliSaganmanatlebloProgramebi from "./pages/Profesiuli-saganmanatleblo-programebi.svelte";
  import ProfesiuliStudentisGzamkvlevi from "./pages/Profesiuli-studentis-gzamkvlevi.svelte";
  import SamoqmedoGegmebi from "./pages/Samoqmedo-gegmebi.svelte";
  import SasertifikatoProgramebi from "./pages/Sasertifikato-programebi.svelte";
  import SastsavloKhelshekrulebisNimushi from "./pages/Sastsavlo-khelshekrulebis-nimushi.svelte";
  import Sertifikati from "./pages/Sertifikati.svelte";
  import Struqtura from "./pages/Struqtura.svelte";
  import StudenturiServisebi from "./pages/Studenturi-servisebi.svelte";
  import { footerData } from "./json/footer-data.json";
  import { Router, Link, Route } from "svelte-routing";
  import HaberDetay from "./routes/BlogDetails.svelte";
  let url = "";
  
</script>

<main
  class="text-center py-0 min-h-screen flex flex-col items-center font-georgian"
>
  <Header />
  <Router {url} >
    <Route path="/" component={HomePage} />
    <Route path="/struqtura" component={Struqtura} />
    <Route path="/profesiuli-ganatlebis-mastsavleblisprogramis-ganmakhorcieleblis-samsakhurshi-mighebis-tsesi" component={ProfesiuliGanatlebisMastsavleblisprogramisGanmakhorcieleblisSamsakhurshiMighebisTsesi} />
    <Route path="/profesiuli-mastsavleblis-gzamkvlevebi" component={ProfesiuliMastsavleblisGzamkvlevebi} />
    <Route path="/samoqmedo-gegmebi" component={SamoqmedoGegmebi} />
    <Route path="/maregulirebeli-aqtebi" component={MaregulirebeliAqtebi} />
    <Route path="/avtorizaciis-gadatsyvetileba" component={AvtorizaciisGadatsyvetileba} />
    <Route path="/administracia" component={Administracia} />
    <Route path="/profesiuli-mastsavleblebi" component={ProfesiuliMastsavleblebi} />
    <Route path="/partniorebi" component={Partniorebi} />
    <Route path="/misia-khedva-ghirebulebebi" component={MisiaKhedvaGhirebulebebi} />
    <Route path="/profesiuli-saganmanatleblo-programebi" component={ProfesiuliSaganmanatlebloProgramebi} />
    <Route path="/profesiuli-momzadebisprofesiuli-gadamzadebis-programebi" component={ProfesiuliMomzadebisprofesiuliGadamzadebisProgramebi} />
    <Route path="/sasertifikato-programebi" component={SasertifikatoProgramebi} />
    <Route path="/profesiuli-studentis-gzamkvlevi" component={ProfesiuliStudentisGzamkvlevi} />
    <Route path="/msmenelis-gzamkvlevi" component={MsmenelisGzamkvlevi} />
    <Route path="/studenturi-servisebi" component={StudenturiServisebi} />
    <Route path="/informacia-ssm-da-shshm-pirebistvis" component={InformaciaSsmdaShshmPirebistvis} />
    <Route path="/sastsavlo-khelshekrulebis-nimushi" component={SastsavloKhelshekrulebisNimushi} />
    <Route path="/kursdamtavrebulebi" component={Kursdamtavrebulebi} />
    <Route path="/diplomi" component={Diplomi} />
    <Route path="/sertifikati" component={Sertifikati} />
    <Route path="/biblioteka" component={Biblioteka} />
    <Route path="/katalogi" component={Katalogi} />
    <Route path="/charickhvis-tsesi" component={CharickhvisTsesi} />
    <Route path="/gzamkvlevi-aplikantebs" component={GzamkvleviAplikantebs} />
    <Route path="/bibliotekis-sargeblobis-tsesi" component={BibliotekisSargeblobisTsesi} />
    <Route path="/eleqtronuli-tsignebi" component={EleqtronuliTsignebi} />
    <Route path="/blog/:id/:slug" component={HaberDetay} />
  </Router>
  <Footer {footerData} />
</main>

<style>
</style>
