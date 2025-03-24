<script>
  export let image;
  export let content;
  export let date;
  let months = [
    "იანვარი",
    "თებერვალი",
    "მარტი",
    "აპრილი",
    "მაისი",
    "ივნისი",
    "ივლისი",
    "აგვისტო",
    "სექტემბერი",
    "ოქტომბერი",
    "ნოემბერი",
    "დეკემბერი",
  ];
</script>

<div class="flex gap-4 md:w-80">
  <img src={image} alt="Haber Resmi" class="h-16 aspect-video object-cover" />
  <div class="text-left">
    <p class="text-base font-bold text-[var(--color-mscaccentdark)]">
      {content.length > 50 ? content.slice(0, 50) + "..." : content}
    </p>

    <span class="text-xs text-[var(--color-mscaccentdark)]"
      >{`${new Date(date).getDate()} ${months[new Date(date).getMonth()].slice(0, 3)} ${new Date(date).getFullYear()}`}</span
    >
  </div>
</div>
