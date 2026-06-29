<script setup>
import { ref, computed, watch } from 'vue'
import { districts } from './data'

const readAgreement1 = ref(false)
const readAgreement2 = ref(false)




const courts4 = computed(() => {
  if (!region4.value) return []

  return [
    ...districts[region4.value],
    region4.value
  ]
})


// STEP
const step = ref(1)

// STEP 1
const firstName = ref('')
const lastName = ref('')
const middleName = ref('')
const phone = ref('')
const email = ref('')

// STEP 2
const region = ref('')
const district = ref('')
const address = ref('')

// STEP 3
const receptionType = ref('')
const leader = ref('')
const courtDirection = ref('')
const participationType = ref('')
const courtRegion = ref('')
const caseDate = ref('')
const partyType = ref('')

const caseFirstName = ref('')
const caseLastName = ref('')
const caseMiddleName = ref('')
const caseNumber = ref('')

// ERROR FLAGS
const step1Error = ref(false)
const step2Error = ref(false)
const step3Error = ref(false)

// STEP 4
const region4 = ref('')
const court4 = ref('')
const decisionDate = ref('')

const step4Error = ref(false)

// STEP 5
const orderNumber = ref(null)
const orderDate = ref('')

const step5Error = ref(false)

// STEP 6
const appealText = ref('')
const selectedFile = ref(null)

const step6Error = ref(false)
const formCompleted = ref(false)

const selectedRegion = ref('')
const couurtRegion = ref('')

const districtList = computed(() => {
  return districts[selectedRegion.value] || []
})

const handleFileUpload = (event) => {
  selectedFile.value = event.target.files[0]
}

// Viloyatga mos tumanlar
const filteredDistricts = computed(() => {
  return districts[region.value] || []
})

watch(region, () => {
  district.value = ''
})

// STEP 1 VALIDATION
const phoneRegex = /^\+998\d{9}$/

const isStep1Valid = computed(() => {
  return (
    firstName.value.trim().length > 1 &&
    lastName.value.trim().length > 1 &&
    middleName.value.trim().length > 1 &&
    phoneRegex.test(phone.value) &&
    email.value.includes('@')
  )
})

const nextStep = () => {

  // STEP 1
  if (step.value === 1) {

    step1Error.value = true

    if (!isStep1Valid.value) {
      alert("Shaxsiy ma'lumotlarni to'liq kiriting")
      return
    }
  }

  // STEP 2
  if (step.value === 2) {

    step2Error.value = true

    if (
      !region.value ||
      !district.value ||
      !address.value.trim()
    ) {
      alert("Yashash manzilini to'liq kiriting")
      return
    }
  }

// STEP 3
if (step.value === 3) {

  step3Error.value = true

  const mainFields =
    receptionType.value &&
    leader.value &&
    courtDirection.value &&
    participationType.value &&
    courtRegion.value &&
    caseDate.value &&
    partyType.value

  const personFields =
    caseFirstName.value &&
    caseLastName.value &&
    caseMiddleName.value &&
    caseNumber.value

  if (!mainFields) {
    alert("Qabul ma'lumotlarini to'lliq kiriting")
    return
  }

  if (!personFields) {
    alert("Ish bo'yicha shaxs ma'lumotlarini to'lliq kiriting")
    return
  }

  if (!readAgreement1.value || !readAgreement2.value) {
    alert("<<men o'qib chiqdim>> belgisini o'qing")
    return
  }
}

// STEP 4
if (step.value === 4) {

  step4Error.value = true

  if (
    !region4.value ||
    !court4.value ||
    !decisionDate.value
  ) {
    alert("Barcha maydonlarni to'ldiring")
    return
  }
}
// STEP 5
if (step.value === 5) {

  step5Error.value = true

  if (
    orderNumber.value == null ||
    orderNumber.value === '' ||
    !orderDate.value
  ) {
    alert("Ajrim raqam va sanasini kiriting")
    return
  }

  step.value++
  return
}

// STEP 6
if (step.value === 6) {

  step6Error.value = true

  if (
    !appealText.value.trim() ||
    !selectedFile.value
  ) {
    alert("Murojaat matni va faylni yuklang")
    return
  }

  formCompleted.value = true
  return
}

step.value++
}
</script>

<template>
  <div class="min-h-screen bg-[#f3f5f8]">
    <!-- HEADER -->
    <header class="bg-white shadow-sm">
      <div class="max-w-6xl mx-auto flex flex-col gap-2 py-6 items-center text-center">
        

        
      <svg  viewBox="0 0 192 202" class="h-24 m-auto w-auto"><defs></defs><path fill="#fc0" d="M96 35v36h-1V35h1zm2 0h1l-2 36a23 23 0 00-1 0zm2 0l1 1-3 35zm3 1h1l-5 35zm2 0l1 1-6 34zm3 1l1 1-8 34v-1zm5 2l1 1-10 32h-1zm2 2h1l-11 32a23 23 0 00-1-1zm2 1l1 1-12 30a23 23 0 00-1 0zm2 2h1l-13 29a24 24 0 00-1 0zm2 1l1 1-15 28zm2 2v1l-15 27v-1zm1 2h1l-16 26a25 25 0 00-1 0zm2 2h1l-17 25a22 22 0 00-1-1zm2 2l-17 23a24 24 0 00-1 0zm2 3v1l-18 21a23 23 0 000-1zm1 2v1l-18 19a25 25 0 00-1 0zm1 2v1l-18 18a24 24 0 00-1 0zm1 3l-19 17a26 26 0 000-1zm1 2v1l-19 15a24 24 0 00-1-1zm0 2l1 1-19 14a26 26 0 00-1-1zm1 2v1l-19 13v-1zm1 4l-19 11a25 25 0 000-1zm0 2v1l-19 9a25 25 0 000-1zm0 2v1l-18 8a25 25 0 000-1zm1 2v1l-19 7a24 24 0 000-1zm0 2v1l-18 6a26 26 0 00-1-1zm0 2v1l-18 5a26 26 0 000-1zm0 2v1l-18 4zm-1 4a56 56 0 010 1l-17 2v-1zm0 2l-16 2a26 26 0 00-1 0zm0 1v1l-16 2a26 26 0 000-1zm-1 2v1l-15 1v-1zm0 2v1h-15v-1zm-78 1v-1h15v1zm0-2a52 52 0 01-1-1l16 1a23 23 0 000 1zm-1-2a53 53 0 010-1l16 2v1zm0-2l16 2zm0-1a56 56 0 01-1-1l17 2v1zm-1-4v-1l18 5zm0-2a54 54 0 010-1l18 5v1zm0-2v-1l18 6v1zm0-2v-1l19 7v1zm0-2v-1l19 8v1zm1-2v-1l19 9-1 1zm0-3l19 10a25 25 0 000 1zm1-3v-1l19 13a28 28 0 000 1zm0-2v-1l20 14a25 25 0 00-1 1zm1-2v-1l19 15v1zm0-3h1l19 16-1 1zm1-2l1-1 19 19h-1zm1-2l1-1 18 20zm1-2l1-1 18 21v1zm3-4l18 23h-1zm1-2h1l16 24v1zm2-2l16 26zm1-1l1-1 15 27-1 1-15-27zm2-2l1-1 14 29h-1zm2-2h1l13 29h-1zm2-1l1-1 12 31h-1zm2-2h1l11 31-1 1zm2-1l1-1 10 33h-1zm5-2l1-1 7 34-1 1-7-34zm3-1v-1l6 35h-1zm2-1h1l4 35h-1zm2 0l1-1 3 36h-1zm3-1h1l1 36a23 23 0 00-1 0zm3 81c12 0 22-10 22-22 0-11-10-21-22-21S74 83 74 94c0 12 10 22 22 22"></path><path fill="#128c49" d="M61 106c2 0-1-2 0 0l10 11c2 2 2 5 2 7 2 4 8 4 12 4 10 0 21 4 30 0 4-2 4-6 6-10 2-5 7-8 10-12h-30c-9-2-16-2-25-2l-15 2"></path><path fill="#165016" d="M70 113l3-1 1 2v-1l-4 1m1-6c0-2 2-2 3-1l1 1h-4m11 8c1-1 3-2 4-1l1 1h-5m0-5l4-1 1 2-1-1h-4m-2-2l4-1 1 2-1-1c-1 0-3-1-4 1m-2 16l4-1 1 2-1-1h-4m-3-4l3-1 1 2-1-1-3 1m7-3h3l1 1-1-1-3 1m29 5l3-1 1 2v-1h-4m-6-11l3-1 1 2v-1h-4m-2-2l3-1 1 2v-1h-4m2-2l4-1v1c-1 0-3-1-4 1m14 1c0-1 2-2 3-1l1 1h-4m1-2l3-1 1 2v-1h-4m-15 8c0-2 3-2 4-2l1 2c1 0 0 0 0 0-2-1-4-2-5 0m2 2c1-1 3-2 4-1l2 2-1-1c-2 0-4-1-5 1m-32 2l5-1 1 2v-1c-2 0-4-1-6 1m3-2l5-2 1 3v-1h-6m-2-2c1-1 3-2 5-1l1 2-1-1c-1 0-4-1-5 1m3-3c1-2 3-2 4-1l2 2-1-1h-5m-12-8l5-1 1 2-1-1c-1 0-4-1-5 1m-1-3c0-1 3-2 4-1l1 2v-1c-2 0-4-1-5 1m14 2l4-1 1 2-1-1-4 1v-1m4 5l4-1 1 2-1-1c-1 0-3-1-4 1v-1m0 5l3-1 1 2v-1h-4m-2 3l4-1 1 2-1-1h-4m32-1l4-1 1 2-1-1c-1 0-3-1-4 1v-1m-6 3l3-1 1 2v-1h-4m-2-4c0-1 2-2 3-1l1 1h-4m3 1l4-1 2 2-1-1c-2 0-4-1-5 1v-1m3-2l4-1 2 2-1-1c-2 0-4-1-5 1v-1"></path><path fill="#0099b5" stroke="#000" stroke-width=".7" d="M57 99l8-1h6c4-1 7-7 11-5 7 2 16 8 23 2 2-1 3 1 5 2h6l7 1 1 1 7 1 4 1v0l-1 1c-1 2-1 4-3 4l-6 1h-18l-9-1H60c-2-1-3-7-3-7"></path><path fill="#fff" d="M111 107c3 1 10 4 7 6s-4 1 3 5l-3 4s-14-7-7-8 5-4-1-7zm-30-1c-3 1-10 4-8 5 4 3 5 1-2 5l2 5s15-8 8-9c-7 0-5-3 1-6z"></path><path fill-rule="evenodd" d="M125 38c-2-3-7-9-8-15l-1-2a8 8 0 00-1-1 8 8 0 00-2-1l14-2a19 19 0 018 1h-2l-4-5s13 4 15 6v-2a105 105 0 005 4l7 6v-3s10 10 12 14v-1l7 12 1-2 7 16 1-2 1 4v1l3 13s2 1 3 13l-1 16 1-2-2 14 2-1-6 17s-4 16-15 27h2s-6 9-11 11h2l-10 8-1 1-2 1 2 1-9 5-6 3 1 1-9 3-6 1-5-1-7 4H98s0-5-4-6c-4 1-4 6-4 6-9 0-20-3-20-3l-1-3-4 2-1-1v-2l-2 2c-2-2-1-3-1-3h-2c-8 0-10-3-10-3l1-2-4-5h-7l1-2-4-1a11 11 0 01-1-2v-1l-6-7c-5-2-6-4-5-4s2 0 0-2c-3-2-3-4-3-4h2a91 91 0 01-21-39l-1-6h1c-1-2-2-10 0-10l1-1c-6-7-1-28 0-31l1-1 3-4v-4l2 1c-1-5 1-8 1-8l1 1 4-8 2 1v-5h2l1-1c-1-1 3-3 3-4v-3l2 1c-1-3 4-10 4-10v3l1-1 8-7 2 1c-1-2 6-8 6-8v1l7-4v1c2-2 8-2 8-2l1 1 2-1v3l4-2 1 1 1 2 4 1-2 7 1 1-3 4 1 2-2 2 1 2a516 516 0 0117-3h1C55 43 53 75 53 75c-1 10 1 18 4 24a44 44 0 006 9 41 41 0 002 2l3 3 3 3 4-2 1-1h-1l-2-1v-1l1-2 6-3h3l-5 3-1 1 1 1 3 1 1 1 1 1-2 2-7 5 1 3 3 3 3 1h1l3-3v-1a16 16 0 001-3 23 23 0 001-5v-3-7l1-11 3-3s-11-1-6-13c0 0-1 4 7 4h3l7 2h1c1 0 3 0 3 2 0 0 4 2 4 7l-5-2h-1s0 2-3 2h-2l-1 4a31 31 0 003 10l5 14a11 11 0 001 2l2 2v1l1 1h1c1 0 5-1 6-4v-1h1v-1a58 58 0 01-4-2l-4-2-1-3v-1l2-1h3l1-1-2-2a37 37 0 00-5-3l-7-1c2 0 6-1 8 1h2a36 36 0 001 0l16-1a4 4 0 001 0c1-1-1-2-1-2h2c2-3-2-4-4-5l7 2h1l1-2c3-6 5-14 5-24 0 0-3-32-36-42h2l9 1a47 47 0 0110 4zm-42 68h2-2zm2 0l2-1-2 1zm-6-13l-7 5h-3c4 1 7 3 11 2l1-2h-7l2-1v-1c1 0 3 1 2-1 0-1 2-1 1-2zm35 4h-2c12 1 12 3 11 2h-10l4 2c-3 0-7 2-9 0 0 3-3 3-5 4l5-1 2-1 5-1 9-3-10-2zm-52 2l-4 1c1 2 2 5 4 5l6 1h12c-4 0-9-3-12 0-1-1-3-3-1-4-3 0-4 1-6 3l1-3v-2l1-1h-1zm1 0zm19 2l4 1c1-2-3-1-4-1zm49 5a42 42 0 01-7 7l-4 4-4-2v-1h1l2-1v-1l-1-2-3-2a47 47 0 00-3-1l16-1h3zm-50 0l-3 2-2 2 1 2 4 1h1v2l-2 2a50 50 0 01-6 4l-2-4 4-3v-1-1l-2-1h-1l1-1 2-2 5-2zm30 2a63 63 0 016 2l2 2-1 1-2 1-1 1h1l1 1 3 2-2 4a68 68 0 01-7-5l-1-2 1-1 4-1 1-1-2-3-3-1zm8 5a2 2 0 01-1 0h-1l-1 1 1-1a15 15 0 002 0zm-44 1l-1 1-3 1 3-1 1-1zm-4 2zm17 1zm33 1l-2 5zm-1 0l-2 4zm-1 6v0z"></path><path fill="#fff" d="M69 169c1-5-7-6-11-4-1 0-3 0-5 2s-1 5 1 8c-2 1-2 3-1 5 0 2 4 1 4 2 2 3 6 2 9 2 1-1 2-2 1-4 0 2-2 2-4 2h-2l3-4c-2-1-4-3-4-6l6 1c0-1-1-4 1-5l2 1m-27-9c-2-2-7-1-10 0-2 0-4 3-2 6l3 1c-1 1-2 4-1 5h4c0 3 3 2 5 2l1-1h-2v-4l-5-4 5-1v-4l3 1-1-1m-15-39c0-4-6-4-8-3s-2 4-1 6h-3c-1 1-1 4 1 5-1 2-1 4 1 5l5 1a55 55 0 00-4-3l4-1h2v-6c2 1 4 3 4 5h4c0 2-2 2-3 4 5 1 6-5 5-8l-2-1-1-4h-4M16 72c-1-3-5-3-7-3-2 1-2 4-2 6l-2 1c-3 3 3 6 5 8 0-2 2-4 3-5 1 2 3 3 3 5 1-2 4-2 6-1 1 1-2 2-2 3h3c2-4 1-9-4-9 0-2 2-3 1-4-1-2-3-2-4-1m23-18c-2 0 2-4-3-8-2-1-7-2-8 1l-4 4c-2 1-1 4-1 6l-1 1h1c2 1 2 4 4 2l1-1 3-4 1 4v2c2-1 4 0 5 2l-4 2 1 2c1 1 2-1 3-2l3-3 1-1c2-2 1-7-2-7m7-18c-6-3-4-8-4-8 0-5 5-3 5-3 2-4 7-1 7-1s5-2 6 2c0 0 3 2 1 7 0 0 3 7-3 7 0 0 0 7-5 3 0 0 2-3-1-6 0 0 3-3 3-6l-6 1s1-3-2-5c0 0-2 3-1 8"></path><path fill="#cc6b30" d="M70 171l-3-2v5h-2l-4-1 1 2 4 2-2 2-1 2c2 0 3 0 4-2v-3l2-4 1-1m-26-8a1 1 0 01-1 0l-2-2v4h-2-2v1l2 1 2 2v3l1 1 1-1v-2l-1-2h-1l-1-2 2-1 1-1v-1m-16-30a9 9 0 000-4l-2-2a22 22 0 000 6l-5-1 4 3h3l1-1 3-3h-3l-1 2M16 86c-2-1 4-4 5-2-1 3-3 3-5 2m0-1l-1-2-2-3-1 4 4 1m9-23c1 2 2 2 3 2l-2 1-1-3m6 0c1-1 0-3-1-4l-2 4h-3c1 1 8 3 10 1 1-1-2-2-4-1m17-33s-2 2-1 7h1s0 3 4 5c0 0 1-4-2-4 0 0 3-2 4-5l-5 1-1-4"></path><path fill="#184" d="M68 35c-3 0-5 0-4 4 1-2 3-1 3-4h1m6 132c0-2-3-2-4-3l1 2v3c0-1 1-2 3-2m-6-4c-2-2-6-4-9-4 0 3 3 5 6 5l-4-3 6 3h2l-1-1M10 68l-2-2v3l2-1m21-2s-1 6-5 9l2 1 5-2 1 3 5-13-1 3-4 2c-2 1 0-1-3-3m-2-2h2s-1 7-8 13l-2-1s5-3 8-12m-10-7s3-1 2-6c0 0-1-3-2 0l-2 2 2 4m4-14l3 4v1l-4-3s3 2 3 4l-1 1s-2-2-5-2l-1 2v-3h3v-4m27-4l-3 1v1l4-1m-6-5l-1 4h1l1-4m4 3v-1h-1l-4 3h1s2-2 4-2m-2-20v6s-4-1-5 1v1l-1-1s2-4 4-5m15-5s-4 4-4 6l-1 1h-2s1-5 2-6c0 0-3 2-4 5l-3 1v-4l5-3 1 1 6-2h1m-8 166c-2 0-3 2-5 3l6 5-1 1c3 3 7 2 11 2v1l-1 2 1-1c3 1 3-2 5-3v-7l-3 5-1 1 2-4h-6-1l-2-2c-2-1-5 0-8 1l2-2h4l-3-2m-11-5h-3l-2 3 5 2v1l-1 1c3 1 5 1 8-1l3-3-3-1h-6l-4 1c2-2 4-2 6-2l-2-1h-1m-27-48l-5-6H3l2 4v4c2 3 6 3 9 5h1v-1l-7-4 3 1 3 1v-1l-9-4 7 2 2 1v-2m1-5l-1 1-1 2c-1-1-3-3-2-4s3 0 4 1m6-10l1 5h1v-4h-2m-3-1l2 4h1l-1-4h-2m-3-59s4 4 4 7l4-1v8l4-1s-1 4-4 6v-3l-1 3h-1l-1-1 2-4h-2l-2 3 1-3h-1l-1-7h-1l1 8h-1l-1-5v3h-1l-1-3h-1l1 5h-2l-1-4 1-4 1 1 3-6v-2m28-12l2 1s3-2 6-1v2l3 2s-9 7-12 12c0 0 1-3-1-4-1 0 0 0 0 0l5-3s-3 0-5 2h-1s1-3 9-7c0 0-4-1-10 5 0 0-1-4-3-4 0 0 4-2 5-5v-1l2 1"></path><path fill="#00af3e" d="M69 179l1 11m-38-89v7M2 87v8m32 63l-13-2 4 5h-2c0 2 2 3 4 3v1l-2 1c1 2 3 3 4 2s-1-1-1-1v-3l-2-1c2 0 2-1 3-3l-5-2h1c2 1 4 2 5 1l4-1m23 6l1-5c-2-1-3 0-4 1s-1-2-2-1l-1 2c-3-3-6-2-9-2 1 2 3 3 3 5h-1l-3 1 1 1c1 3 2 5 4 6l-3 3 5 2h3v-5c-1-3-4-4-7-5l5 1c1 0 3 0 2-1-1-2-3-5-6-6 3 0 5 3 7 5h1l-1-4 2 3 3-1m-23-47c-1-2-4-3-6-2h-2l-1-1v3l3 2 1-3 1 3 3 3 1-3-1 4c3 1 3 5 2 8v2l1 1h-3l-3 1h8v-1l-1-1c-1-4 0-7-2-11l-1-5m-16 0c1-2 0-2-2-4v-1a5 5 0 01-1 2l-1-2-5-4v4c-2-1-3-4-6-5v8l3 2H3c-1 1 0 2 1 3h7c-2 0-2-2-3-3l-2-6c1 4 5 6 8 9l-1-4v-2c0 2 2 4 3 5l2-2m10-38c0-2-1-2-2-3l-1 7 2-4-2 7h2l1-1 3-2c-1 3-2 4-5 5l4 1c-1 1-4 0-3 2l3 1 1-1 2-13-1 1v-3h-1l-3 2m12-51l1 4h-2l-1-3 2-1m-3 1s-5 1-7 7l-1-2s-3 3-3 7h-1s0 3 3 5l1-7s-1 3 1 5 0-5 5-9c0 0-3 5-3 9h1s1-2 5-4c0 0-3 2-3 4l1 1s1 0 4-4l1-1h-2l2-6s-2-1-3 1c0 0 1-3-1-6m31-12l-4 2-1-3s-5 2-6 7l2 1s1-2 3-2l-2 2 2 2 5-2s-2 3-4 3v2s3-1 5 1h-5v4l6-1-1-2 3-4-1-1 3-5-4-1c-2-1 0 0 0 0l-1-3"></path><path fill="#0099b5" fill-rule="evenodd" d="M96 2l4 4h6v6l5 5-5 4v6h-6l-4 5-4-5h-7v-6l-4-4 4-5V6h7z"></path><path fill="#fc0" fill-rule="evenodd" d="M96 0l-5 5h-7v7l-5 5 5 5v7h7l5 5 5-5h7v-7l5-5-5-5V5h-7zm0 1l5 5h6v6l5 5-5 4v7h-6l-5 5-5-5h-6v-7l-5-4 5-5V6h6z"></path><path fill="#fff" d="M96 7a10 10 0 000 20 10 10 0 007-4 8 8 0 01-5 2c-4 0-8-4-8-8a8 8 0 018-9l5 2a10 10 0 00-7-3zm8 13l-2-2-2 2v-3l-2-1h3l1-3 1 3h3l-3 1z"></path><g><path fill="#ffd033" d="M106 89l-1 2 4 1-3-3"></path><path fill="#fff200" d="M86 87s-1 0 0 0h0m2 1h-2l2-1v1m2 0l-1 2h-2l2-2h1m2 0c-1 1-1 3-3 2l2-2h1m2 0c-1 1-1 3-3 3l2-3h1m2 0h-1l-2 3c1-1 3-1 3-3"></path><path fill="#fff" fill-rule="evenodd" d="M97 99h-8l-1 5 1-1v1l1-1v1l1-1v1-1l1 1v-1l1 1v-1l1 1 1-1v1-1l1 1v-1l1 1v-1h1zm-9 6c6 1 9 0 11-1l1 6-1-1v2l-1-1v1l-1-1-1 1v-1l-1 1v-1l-1 1-1-1v1l-1-1v1l-1-1v1l-1-1v1l-1-1-1 1v-3zm0 57l2 1h2l3 1h3l2-1c1 1 3 1 3-1h1l-2 5-2-1-1 1-1-1-2 1-1-1-2 1-1-1c1 1 0 1-1 1l-1-1v0l-2-2v-2m-1-6h1l2 1 2 1h5l3 1v-1l2-2v1l4-2-1 2v1l-2 3h-1l-1 1c-1 1-1 0-2-1l-1 2h-2l-1-1v1l-2-1-2-1v-2l-1 2c-2 0-1-2-2-3v1c-2 0-2-2-2-4v1m6 1l1-4 1 4 2 1v-1-2h1l1 2h1v-2h1v1h1l1-1c0-1 0-1 0 0l1 1 2-3c0 2 2 1 2 1l1-5-2 1-1 1h-1-1l-1 1h-2s1 0 0 0h-3l-2 1-2-1-4-1-2-1-2-1 1 4v-1h1c0 1-1 3 1 3v-2h1c0 1-1 3 1 3v-3h1v3l1 1m-10-15l2 1v-1l2 2 1-1c0 2 2 2 3 2l2 1a2 2 0 002-1l3 1 1-1h2a2 2 0 001-1c1 1 2 1 3-1h1l1-1h1l1-1h2l-1 1-1 6h-2v1h-2v1h-1l-1 1h-1v-2h-1l-1 3c-2 0-2-2-2-3l-1 3-3-1v-2 2c-1 1-2 0-3-1v-4h-1v4l-2-4v2h-2v-2l-1 2-1-4-1-2m-2-8l1 5v-5h-1m2 1s-2 1 1 7c0 0 2 1 2-4h1c-1 2-1 5 1 5v-3h1a6 6 0 000 3c0 1 1 2 2 1v-4l1 1 1 4h1l1-3c0 2 1 4 2 3 2-1 1-3 1-4l1 3h2v-1-3h1v2l1 2c2-2 0-5 1-7l1 6h1v-6h1v4h1v-5c2 0 0 3 2 4l1-1-1-5 2 2c0 1 0 0 0 0l-1-5v1h-1v2l-1-1-1 2-1-1-1 2-1-1-2 2-1-1-2 1h-1c-1 2-2 0-3 1-3 1-2 0-3-1l-2 1-2-1-2-1-3-1-1-1m17 2a1 1 0 01-1-1c0-1 1-2-1-3v4h-2v-3h-1v3h-2v-3h-1l-1 3-1-1 1-4h-1v3l-1 1c-1 1-2 0-2-1l1-4-1 2-1 2-1 1v-1l1-5c-1 2-1 4-3 5l1-5v-1l-2 6v-1l3-6 1 1 1 1h2v1l2-1 3 2c1 0 0-2 1-1h6l1-1h3v-1l1 1 1-1 1-1c1 0 0-3 2 2l1 2h-1a43 43 0 00-2-2l2 3c-2 1-2-2-3-3l1 3c0 1 0 2-1 1l-2-3 1 3-1 1-1-2c-1 1 1 3-1 4l-2-4c0 1 1 4-1 4m-12-14l1 1h1l2 1a1 1 0 000-1l2 1h3v-1h2l1 1h1l1-1h2v-1h2l1 2v1l-1 2a1 1 0 010-1c-1 1-1 2-2 1l-1 1-1-1v-1-1h-1v4l-2-1v-1l-2 2-1-1v1l-2-3-1 2v1l-1-1h-2l1-2-2 2h-1v-2-1l-2 2c-1-2 1-3 2-5m1-5h3l3 1v-1h6v-1h2l1 2 1 2v1h-1-1v1h-1l-1-1-1 2-1-1v1l-2-1v-1c0 1 0 3-1 2l-1-1-1 1-1-2-1 1-1-1-1 1c-1 0-2 1-2-3l1-2m1-5v0h5v1l1-1h3a1 1 0 001-1v1l1-1 1 4h-1l-1 1-2-1a1 1 0 010 1l-1-1-1 1-1-1-2 1v-1l-3 1v-2 1h-1v-3h1m10-19s3 1 5-1l1-4-2-1c-1 0 0 0 0 0v3h-4-1-2l-4 2s-4 5-2 6c0 0 1 1 2-1v1l2-1s0 2 2 0l1 1c1-1 0-4 2-5m6-5l-1-2h-1l2 2m-19-3s3 2 5 2c3-1 5-2 11-1v4l-2-1c0-1 1-2 2-1l-1-1h-1l-1 3v-3h-2 1s0 2-2 3v-3h-1c-2 0-7 2-9-2m16 1s-2-2-7-2c0 0-8 1-11-3 0 0-1 3 1 7l1-4s4 3 6 2h10m7 64v2h-1v-3l1 1m0 3c-1 1 0 2 1 2l-2 1-1-1 2-2m5 12c0-1 1-2 2-1 0 0-1 2-2 1m-1-1l2-1-2 1m-1-1l2-2a2 2 0 011 0v1l-3 1m-1-1l3-2c1 1-1 1-2 2h-1m-1-1c1-2 3-3 4-2l-1 1-2 1h-1m-1-2c0-1 2-2 4-1l-4 1m-1-1c1-2 3-3 4-2l-1 1-2 1h-1m8 9l2 1c-1 1-2 0-2-1m-1 3h4l1 1-5-1m-2-1h2-3 1m-8-7c0-1 0-3 1-2l-1 2m9 6l-3 1s-1 0 0 0l3-1c1 0 0 0 0 0m-3-2l-2 3h1s0-2 2-2l-1-1m-1 0l-2 3h1l1-3c1 0 0 0 0 0m-1-1s-2 1-2 4c0 0 0 1 0 0 1-1 0-3 3-4h-1m-1-2s-2 2-3 6h1c1-1 0-4 3-5l-1-1m-1-2s-3 3-4 7c0 0 0 2 1 1s1-5 3-7v-1m-1-4l8 9s1 3-2-1l-6-7v-1m4-13c1 1 2 1 1 2h-1v-1-1m12-23v2h4l1-3-4 1m-11 18s9-6 9-16c0 0 1 10-9 17m0 1c1 1 2 2 1 3l-2-1v-2h1m2-1c1 1 3 2 1 3l-2-1v-3m3-1c1 1 3 2 1 3l-2-1v-2m3-2c1 1 3 2 1 3h-2v-3m2-2c1 1 3 1 2 3h-2l-1-3m2-2c2 1 4 1 3 3h-2c-1-1-2-2-1-3m2-2c1 1 3 1 2 2l-2 1-1-3m1-2h3v2h-2l-2-2m1-4h4c2 3-2 4-4 3v-2m1-5c1-1 3-5 4-3 1 1-2 4-4 3m-12 27v2s-2 0-1-1l1-1m3-2v3l-2-1 1-2m3-2v3c-1 1-2-1-2-1l1-1m3-3v3c-1 1-2-1-2-2l2-1m1-2c1 1 3 2 2 3s-3 0-3-1l1-1m3-3l1 2h-3l2-2m1-2l2 1v1c-1 1-3 0-3-1l1-1m2-3l2 1v2l-3-1 1-2m1-4c2 0 4 0 3 2l-1 1h-3l1-2m1-4c1 0 4-2 4 0s-1 3-5 2l1-2m0-4c2 0 4-2 5-1 1 2-2 4-5 3l1-2m-1-3c1-2 4-4 5-3 1 2-2 5-4 4l-1-1m-16 31v3c-1 1-1-2-1-2v-1h1m3 0v2h-1l-1-2h1m3-2v2h-1l-1-1 2-1m3-2v2c-1 1-2 0-3-1l3-1m2-3c1 1 2 3 0 3-1 1-2 0-2-2 1 1 1 0 2-1m2-3l2 1v3h-2l-1-2 1-2m-12 13v2s-1 2-2 0v-1l2-1m2 0l1 1-2 1v-2h1m2-2l1 2s-1 2-2 1v-1l1-2m2-1l2 1s-1 3-3 1v-1l1-1m3-2l2 2s-1 2-3 1l-1-2 2-1m3-2l1 2s-1 3-2 1l-1-1 2-2m2-2l2 2s-1 2-3 1l-1-1 2-2m2-2l2 2s-1 3-2 1l-1-1 1-2m2-3l2 2s0 3-2 2l-2-1 2-3m2-3l3 1s1 3-2 3l-2-1s2-2 1-3m2-3l3 1s1 2-2 1h-2s2-1 1-2m1-3h4s1 3-3 3l-2-1s2-1 1-2m2-4h3s2 2-2 3h-2s2-2 1-3m-3-9h3c0-1 1 2-1 3-3 1-3-1-3-1s2-1 1-2m-6 21l1 1c1 0-1 3-2 2-3-2-1-2-1-2l2-1m1-4l2 1c1-1 1 3-1 3-3 0-2-2-2-2s2 0 1-2m2-3h2c1-1 1 4-1 3-3 0-2-1-2-1s1-1 1-2m2-5h2l-1 4c-5 1-2-2-2-2s1 0 1-2m1-4l2-1c1 0 1 2-1 3h-3l2-2m4-1l3-1c1-1 2 3 0 4-3 2-4 1-4 1s2-3 1-4m-24 35a76 76 0 005 9l-3-2-3-7h1m1-1a77 77 0 005 9s-1 1-3-2l-2-6v-1m1-1a79 79 0 005 9s0 2-2-2l-3-6v-1m2-1a71 71 0 006 9s-1 2-4-2l-3-6 1-1m2 0a68 68 0 005 8s0 2-3-2l-3-5 1-1m1-1l6 7 1 1s-1 1-4-2l-3-6m2-2l6 8 1 1s-1 1-4-2l-3-6v-1m2-1l5 7 1 2-3-2-4-6 1-1m1 0l6 6 1 1-4-2-3-4v-1m3-1l6 5 1 1-4-2-4-4h1m-1 0l6 6 1 1s-1 1-4-2l-3-4v-1m2-2a101 101 0 007 6s-1 1-4-1l-3-4v-1m1-1l7 5 1 1-4-2-5-4h1m1-2l8 5 1 1s-1 1-5-1l-5-4 1-1m1-1l8 5 1 1s-1 1-5-2l-4-3v-1m2-1a71 71 0 009 5s-1 1-5-1l-5-4h1m1-1a82 82 0 009 4s-1 1-5-1l-5-3h1m1-2a83 83 0 0010 4s-1 1-6-1l-5-3h1m1-2a83 83 0 0010 4h-5l-6-3 1-1m1-1a83 83 0 0011 3h-6l-6-3h1m0-2a108 108 0 0014 2l-7 1-7-2v-1m1-2l12 1 2 1-7 1-7-1v-2m1-2h11l3 1-7 1h-8l1-2m0-1l14-2c1-1 0 0 0 0s-1 2-6 2h-8m15-4h-7l-8 2s13 0 15-2m2-6l-15 5-1 1 13-3 3-3m-15 2v2s13-3 15-6c0 0-5-1-15 4m1-4l10-5s2-2 5-1c0 0-1 4-6 5l-9 3v-2m-6 1l4-2c1-1 2 2-2 4l-2 1v-3m5-3l11-8 6-2-5 5-10 6h-2v-1m1-4s12-12 16-12c0 0 0 3-4 5l-12 9v-2m-16 6l4-3s2-1 1 1-4 3-5 3v-1m6-3l3-2s2 0 0 4c-2 2-3 1-3 1v-3m5-2l3-3s3 1 0 6l-4 2 1-5m-6 0l3-4s2-2 1 3c-2 4-4 1-4 1m5-4l3-3c1-2 2 1 0 4s-3 2-3 2v-3m5 0l10-11 6-4s1 3-6 8l-9 9-1-2m0-3l6-9c1-2 4-8 9-9 0 0-1 6-5 10l-9 9-1-1m-6 1l3-7s2 0 1 3c0 0-2 6-4 4m5-5s9-14 10-18l2-4s1 7-2 11l-10 13m4-33l2-5c1-1 1 0 3 6s-2 18-5 22l-4 6s3-8 4-15V68m-4 13s1 12-8 23l-9 11s-4 3-4 8c0 0-1 6-8 7 0 0 2 3 1 6-2 3 8-6 8-13 0 0 1-5 5-8 5-4 8-10 8-10s9-14 7-25m-27-44s34 14 26 59c0 0 21-44-26-60h-2M83 150v2h1v-3l-1 1m1 3l-1 2 1 1 1-1-1-2m-6 12c0-1-1-2-2-1 0 0 1 2 2 1h1m0-1c-1-1-1-2-2-1l2 1m1-1l-1-2a2 2 0 00-2 0l1 1 2 1m1-1c-1-1-2-3-3-2s1 1 2 2h1m1-1c-1-2-2-3-3-2l1 1 1 1h1m1-2c0-1-2-2-4-1l4 1m1-1c-1-2-3-3-4-2l1 1 2 1h1m-8 9l-1 1 1-1m1 3h-4l-1 1 5-1m2-1h-2 2m8-7c0-1 0-3-1-2l1 2m-9 6l3 1s1 0 0 0l-3-1m3-2l2 3h-1l-1-2v-1m1 0l2 3h-1l-1-3c-1 0 0 0 0 0m1-1s2 1 3 4h-1c-1-1 0-3-2-4-1 0 0 0 0 0m1-2s3 2 3 6h-1c-1-1 0-4-2-5v-1m1-2s3 3 4 7c0 0 0 2-1 1s0-5-3-7v-1m1-4l-8 9s-1 3 3-1l5-7v-1m-4-13c-1 1-2 1-1 2h1v-1-1m-12-23v2h-4l-1-3 5 1m10 18s-9-6-9-16c0 0-1 10 9 17v-1m0 2c0 1-2 2-1 3l2-1v-2h-1m-2-1c0 1-2 2-1 3l2-1v-3m-2-1c-1 1-3 2-2 3l2-1v-2m-2-2c-1 1-3 2-2 3h2v-3m-2-2c-1 1-3 1-2 3h2l1-3m-2-2c-1 1-3 1-2 3h2v-3m-1-2c-2 1-4 1-3 2l2 1c1-1 2-2 1-3m-1-2h-3v2a3 3 0 002 0l2-2m-1-4h-4c-2 3 3 4 5 3l-1-2m-1-5c-1-1-2-5-4-3-1 1 2 4 4 3m12 27v2l2-1-2-1m-2-2c-2 0-1 2-1 3l2-1-1-2m-2-2l-1 3c1 1 2-1 2-1l-1-1m-3-3v3c1 1 2-1 2-2l-2-1m-1-2c-1 1-3 2-1 3l2-1-1-1m-2-3l-2 2h3l-1-2m-2-2l-2 1v1c1 1 3 0 3-1l-1-1m-2-3l-2 1v2l3-1-1-2m-1-4c-1 0-4 0-3 2l1 1h3l-1-2m-1-4c-1 0-4-2-4 0s2 3 5 2l-1-2m0-4l-4-1c-2 2 1 4 4 3l-1-2m1-3c-1-2-3-4-5-3-1 2 2 5 4 4l1-1m16 31v3c1 1 2-2 1-2v-1h-1m-2 0l-1 2h1c1 0 2-1 1-2h-1m-3-2v2h1l1-1-2-1m-2-2c-1 0-2 1-1 2s3 0 3-1l-2-1m-3-3c-1 1-2 3 0 3 1 1 2 0 2-2-1 1-1 0-2-1m-2-3l-2 1v3h2l1-2-1-2m12 13v2s1 2 2 0v-1l-2-1m-2 0l-1 1 2 1 1-2h-2m-2-2l-1 2s1 2 2 1v-1l-1-2m-2-1l-2 1s1 3 3 1l1-1-2-1m-3-2l-1 2s1 2 2 1l1-2-2-1m-2-2l-2 2s1 3 2 1l1-1-1-2m-3-2l-2 2s1 2 3 1l1-1-2-2m-1-2l-3 2s1 3 2 1l1-1v-2m-3-3l-2 2s0 3 2 2l2-1-2-3m-2-3l-3 1s-1 3 2 3l2-1s-2-2-1-3m-2-3l-3 1s-1 2 2 1h2s-2-1-1-2m-1-3h-4s-1 3 3 3l2-1s-2-1-1-2m-1-4h-4s-2 2 2 3h2s-1-2 0-3m2-9h-3c0-1-1 2 2 3 2 1 2-1 2-1s-2-1-1-2m6 21l-1 1c-1 0 2 3 3 2 2-2 0-2 0-2l-2-1m-1-4l-2 1c-1-1-1 3 1 3 3 0 2-2 2-2s-1 0-1-2m-2-3h-2c-1-1-1 4 1 3 3 0 2-1 2-1s-1-1-1-2m-2-5h-2l1 4c5 1 2-2 2-2s-1 0-1-2m0-4l-3-1c-1 0-1 2 1 3h3l-1-2m-5-1l-3-1c-1-1-2 3 1 4 2 2 3 1 3 1s-2-3-1-4m24 35l-4 7-1 2s2 0 3-2l3-7h-1m-1-1l-4 8-1 1s1 1 3-2l3-6-1-1m-1-1l-4 8-1 1s0 2 3-2l2-6v-1m-2-1l-5 8v1s0 2 3-2l3-6-1-1m-1 0l-5 7-1 1s0 2 3-2l3-5v-1m-2-1l-6 7-1 1s1 1 4-2l3-6m-2-2l-6 8-1 1s1 1 4-2l3-6v-1m-2-1l-5 7-1 2 3-2 4-6-1-1m-1 0l-6 6-1 1s1 1 4-2l3-4v-1m-3-1l-6 5-1 1s1 1 4-2l4-4h-1m1 0l-6 6-1 1s1 1 4-2l4-4-1-1m-2-2l-6 5-1 1s1 1 4-1l3-4v-1m-1-1l-7 5-1 1 4-2 5-4h-1m-1-2l-8 5-1 1s1 1 5-1l5-4-1-1m-1-1l-8 5-1 1s1 1 5-2l4-3v-1m-1-1l-8 4-1 1 5-1 4-4m-1-1l-9 3-1 1s1 1 5-1l5-3m-1-2l-10 3-1 1s1 1 6-1l5-3m-2-2l-9 4h-1 6l5-3-1-1m0-1l-10 2-2 1h6l6-3m-1-2l-12 2h-2l7 1 8-2-1-1m-1-2l-12 1-2 1 7 1 7-1v-2m-1-2H41l-2 1 6 1h8l-1-2m0-1l-13-2h-1s1 2 6 2h8m-15-4h7l8 2s-13 0-15-2m-2-6l15 5 1 1-13-3-3-3m15 2v2s-13-3-15-6c0 0 5-1 15 4m-1-4l-10-5s-2-2-5-1c0 0 1 4 6 5l9 3v-2m6 1l-4-2c-1-1-2 2 2 4l3 1s-2-2-1-3m-5-3l-11-8-5-2s0 2 4 5l10 6h2v-1m-1-4S37 97 34 97c0 0-1 3 3 5l12 9v-2m16 6l-4-3s-2-1-1 1 4 3 5 3v-1m-6-3l-3-2s-2 0 0 4c2 2 4 1 4 1l-1-3m-4-2l-4-3s-3 1 0 6l4 2s-2-5 0-5m6 0l-3-4s-3-2-1 3c1 4 3 1 4 1m-5-4l-4-3c-1-2-2 1 0 4s3 2 3 2l1-3m-6 0L40 95l-6-4s-1 3 6 8l9 9 1-2m0-3l-6-9c-1-2-3-8-8-9 0 0 0 6 5 10l8 9 1-1m6 1l-3-7s-1 0-1 3c0 0 2 6 4 4m-5-5s-9-14-10-18l-2-4s-1 7 2 11l10 13m-4-33l-2-5c-1-1-1 0-3 6s2 18 5 22l4 6h1s-4-8-5-15V68m5 13s-1 12 7 23l9 11s4 3 4 8c0 0 1 6 8 7 0 0-2 3-1 6 2 3-8-6-8-13 0 0 0-5-5-8-5-4-8-10-8-10s-8-14-6-25v1m26-45S44 50 52 95c0 0-21-44 26-60h3"></path></g><g><path fill="#1eb53a" d="M94 194s5 2 5 6c0 0 15-1 17-3l-10 1 10-1h-11l9-1h-9 7l-18-2m-1 0s-5 2-4 6c0 0-15-1-18-3l11 1-10-1h10l-8-1h8l-6-1 17-1m1-8s-20 1-24 4v1l5-1-5 2v1l5-2-5 2v1l6-2-6 2 1 2s10-3 23-3 23 3 23 3v-2l-6-2 6 2v-1l-5-2 5 2v-1l-5-2 5 1 1-2c-10-3-24-3-24-3zm77-28c-5 2-21 2-21 2l-21-1 3-2h5-4v-1l6-1a330 330 0 01-4-1l23-1c9 1 18-1 18-1-1 3-5 2-7 3h4v1h-2l-3 1h4l-3 1h2m-150-3c5 2 17 2 17 2h21l-3-2-5-1h4l-1-1-6-1 6 1-2-2-18-1c-9 1-17-1-17-1 0 3 4 2 6 3h-4v1h2l3 1h-4l4 1h-3s-1 0 0 0m153-42l-10 2-6 3 1-1 4-3-2 1-2 1v-2l4-2-4 1v-2c3-2 16-5 16-5 13-4 14-8 14-8v2l-3 3c-2 1-4 1-4 3l7-4-4 4-2 1 5-2-2 2-6 2 4-1h3v-1c-3 4-8 4-12 5m-158-3l10 3 6 3-1-1-4-3h2l2 2v-2l-4-2 4 1v-2c-3-3-16-5-16-5-13-4-14-8-14-8v2l4 3 3 2-7-3 4 4h2c-2 1-3 0-5-1l2 2c2 1 5 0 6 2l-4-1-3-1c3 4 8 4 12 5"></path><path fill="#0099b5" d="M91 170c-13 0-22 3-22 3v2c2-2 4-1 4-1l-4 1v2l4-1c-5 1-4 3-4 3 4-4 25-4 25-4s21 0 25 5c0 0 0-3-4-4l3 1v-2l-3-1s2-1 3 1v-2s-10-4-24-3a79 79 0 00-3 0zm52-24s-1 0 4-1h-3l1-1h5l-4-1h1l4-1h-4l1-1c3-2 20-1 20-1 11-1 17-4 17-4l-5 4 3-1c0 2-2 3-4 3h3c0 2-2 2-3 2 0 0-8 2-18 2h-18m-98-3s1 0-4-1h3l-1-1-5-1h3l-4-1h4l-1-1c-3-2-15-1-15-1-12-1-17-5-17-5 0 3 3 3 5 5l-4-1c0 2 3 3 5 3h-4l3 2s8 2 19 2h13m115-38v-3l3-3-2 1 4-3-4 1 1-1s5-5 15-7c0 0 8-2 11-8v2l-3 4-1 1 1-1 3-2-2 2-3 3 6-3v3s-8 5-15 6c0 0-8 2-14 8m-129-4v-2l-3-3 2 1-4-3 4 1v-1s-6-5-16-7c0 0-8-2-11-8v1l3 5 1 1-1-1-3-2 2 2 3 2-6-2v2s9 6 15 7c0 0 9 2 14 7"></path><path fill="#fff" d="M94 175s-21 0-25 4l1 11c4-3 24-4 24-4s14 0 24 3l1-10c-4-4-25-4-25-4zm49-29l-7 8 23-1c8 1 17-1 17-1 2-1 6-9 6-9l-3 1-18 2h-18m-98-3l7 8-18-1c-9 1-18-1-18-1l-5-9 2 1 18 2h14m114-38v6c3-2 16-5 16-5 13-4 14-8 14-8v-7s-8 5-15 6c0 0-8 2-14 8m-128-4v7c-3-3-16-5-16-5-13-4-14-8-14-8v-8s9 6 15 7c0 0 9 2 14 7"></path><path fill="#fc0" d="M71 184v-1-1l1-1h3l1 1v3l-1 1h-2-1v-1l-1-1zm4-1v-1h-1v-1h-1v1h-1v2l1 1h2v-1-1zm2-2v1h-1v-2h1zm1 4v-2l1-1v-1-1h-1v1-1l3-1v1l-1 1v1l-1 1v1h2v-1 1zm6-1h-2v-4-1h3l1 1h-1v1h1v2l-1 1h-1zm0-3v-1-1h-1v4h2v-1h-1v-1zm6 2v1h-4v-1h1l-1-4 3-1v1h0-1v1h1v1h-1v2h2v-1 1zm1 1l-1-1h1v-4l-1-1h2v5zm3-1h-1v-1l-1-1v-1h1v-1-1h2l-1 1-1 1 1 1v1l1 1zm2 0v-4-1h1v5h1zm4 1v-1h-1-1v-1h1v1h1l1-1-1-1h-1v-1-1-1h2q0 1 0 0h1v2l-1-1h-1v1h1v1h1v1l-1 1-1 1zm7-4h-1v-1l-1 1v4h-2v-1h1v-4h-1v0h4v1zm0 2v-1l1-1h3l1 1v2l-1 1-1 1h-1l-1-1h-1v-1-1zm4 0v-1l-1-1h-1v1h-1v3h2v-1l1-1zm6 0v1l-1 1v2h-1v-1l-1-1v-1l-1-1v4h-1v-1l1-4v-1l1 1 1 1v2h1v-1-1-1h1v1z" font-family="AR JULIAN" font-weight="400" letter-spacing="0" word-spacing="0"></path><path fill="#ce1126" stroke="#ce1126" stroke-width=".2" d="M94 186a11 11 0 000 0H84l-14 3v1l10-2 11-1a126 126 0 013 0h0a140 140 0 019 0c5 0 11 1 15 3v-1c-8-3-20-3-24-3zm0-11s-12 0-20 2l-5 2v1c1-2 5-3 9-3a116 116 0 0116-2h0a137 137 0 0119 2l6 3v-1l-6-2-8-2a139 139 0 00-11 0h0zm42-21l8-1a263 263 0 0115 0h6a72 72 0 008 0l3-1h0l-11 1h-6-4a262 262 0 00-19 1h0m46-11l-3 1h0s-8 2-18 2a679 679 0 00-18 1v-1h6a683 683 0 0125-1l5-1h0l3-1h0m-130 8l-15-1h-3 0a49 49 0 01-5 0l-13-1h0a57 57 0 0013 1h8l15 1h0m-41-11h2v1-1l5 1a115 115 0 0013 2h14v1l-14-1c-10 0-18-2-18-2h0l-2-1h0m178-49s-8 5-15 6h-1c-3 1-9 3-13 8h0-1v-1h1v1l-1-1c6-5 15-7 15-7h0l10-4a58 58 0 003-2l2-1v1m-30 20l9-4 7-1h0l12-5a9 9 0 002-3h0s-1 4-14 8h0l-7 2-9 3h0M2 87a35 35 0 002 1c2 2 8 5 13 6h0s9 2 15 7h-1 1v1h-1 0l-9-6a39 39 0 00-4-2 22 22 0 00-1 0h0c-7-1-15-7-15-7h0m30 21l-9-3a115 115 0 00-7-2h0C3 99 2 95 2 95h0c0 1 3 4 14 8h0l7 1c4 1 7 2 9 4h0"></path></g><g><path fill="#fc0" d="M118 20s23-2 21 7c0 0-1 5-6 2 0 0-13-9-15-9m17-3s13 2 12 12c0 0 0 3-5-3l-7-9m12 5s12 5 10 15c0 0-2 2-6-4l-4-11m12 8s11 9 8 18c0 0-5 1-7-6l-1-12m11 12s9 11 3 19c0 0-4-1-4-8l1-11m-18 4s20 1 13 10c0 0-3 1-8-4l-5-6m9 11s16 2 12 11c0 0-3 1-8-5l-4-6m6 11s15 5 11 13c0 0-4 1-7-6l-4-7m10-16s8 18 2 21c0 0-4 1-4-7l2-14m7 15s5 17-2 20c0 0-5 2-3-6l5-14m-35-33s2-3-9-3l-8-1s15 11 17 4m9 8s2-3-8-4l-8-1s13 13 16 5m-7 10s4-3-4-10c0 0-4-1-5-3 0 0 2 17 9 13m-9-3s3-3-6-8c0 0-4 0-5-2 0 0 4 11 11 10m9 12s3-4-6-8c0 0-4 0-5-2 0 0 4 11 11 10m7 11s3-3-4-7l-5-2s3 10 9 9m5 15s3-2-3-8l-5-5s2 12 8 13m-36-52s3-3-5-11l-4-3s2 13 9 14m13 6s2-4-7-9l-5-3s4 12 12 12m19 23s4-2-1-9c0 0-4-2-4-4 0 0-2 16 5 13m6 15s5-1 0-11l-3-7s-5 19 3 18m3 12s5-1 1-11v-5s-9 17-1 16m7-2s6 0 0-8c0 0-4-2-4-4 0 0-2 11 4 12m-16-1s5 4 4 5l-3 2s-2-8-1-7m22 25l-1-1-1 1h-1l-4 1 1 1 3 4c2 1 3-1 3-2l1-4h-1m7-4h-1l-2 1c-1 1-3 2-2 3 2 2 4 0 5-2v-2m2 1l-3 5c-2 3-8 6-7 9 1 5 5 0 7-2l2-4c-1-2 1-6 1-8m-2 13c-2 3-5 6-9 8l-1 1-1 3c-1 2 2 2 3 2l3-2c2-1 3-2 3-5l2-7m-15-7c1 5-3 15 4 14 3-1 2-5 1-7s-2-5-5-7m-2-1c-1-1-4 1-4 1-2 2-2 4-1 5 1 2 3 0 3-1 1-2 3-4 2-5m1 5c-3 3-7 4-9 7l-1 2c-1 1 0 2 1 2 3 1 5-2 7-4v-1l2-6m-27 47c-2 3-7 7-8 10l-1 2 1 2c4 1 5-2 6-5v-1l2-8m-9 7l-10 9-1 2 1 3c3 0 5-2 7-5v-1l3-8m22 2l-6 1h-6c1 0-6 3-3 6 3 2 5 1 8-1h1l6-6m-23 17c-4 1-8-4-12-3 1 0-8 3-4 5 3 2 4 2 7 1h2l7-3m34-28c-3 2-9 0-12 2 1 0-6 4-3 7 3 2 6-1 9-2v-1l6-6m-19 20c-4 1-10-2-13-1 0 0-7 3-5 6 2 2 6 0 9-1h1l8-4m24-48l-4 1c-1-4-1-8 1-11l2 4 2 6h-1m-5-8c-2 3-5 3-7 4l-3 4c2 1 4 2 6 1s2-3 2-4l2-4m-12-8v1c-1 4-4 9-1 13 1 1 3-1 3-3 1-4 0-8-2-11m-4 12l-2 5 2-1 1-4m9-16h-3c-1 2-1 6 1 7s2-2 2-3l1-1-1-3m-9 44h-3c-3 3-6 9-3 11 5 4 6-7 6-11m3-1h4c0 3-3 6-5 5-1-1 0-4 1-5m13 0h-7v3c3 1 6 0 7-3m-22 1c-3 0-9-2-7 1 1 1 6 2 7-1m-12-1h3c0 2-2 2-4 2l1-2m-6 0c-2 2-6 5-4 8 2 2 5-2 6-4l1-1 1-3h-4m-4 2c-3 0-7 1-7 4l3 3 4-7m10 10c-4-1-7-2-11-1-2 0-2 3-1 4 1 2 3 2 5 1l7-4m8-8c-4 1-14-1-11 4 2 4 8-1 11-4m-18 14l-2-1-3-2v3c1 1 4 2 5 0m0 1l-5 4c-2 1-1 4-1 6l2-2 4-8" font-family="AR JULIAN" font-weight="400" letter-spacing="0" word-spacing="0"></path><path fill="#540" d="M126 180l-5 4-1 4v2l1-1 1-1 4-8-4 8-1 1-1 1v2-2l-1-2 2-5 5-3m0-1a2 2 0 01-1 0 2 2 0 01-1 0l-3-2v-1 3l2 1 2-2 1 1-3 1-2-1v1a1 1 0 01-1-1v-3h1l4 2h-1 2v1m18-14v1h-3-7l-1 1v2l2 1 5-2 4-3v1-1 1l-4 3-5 2-3-2v-1l1-2 6-1h6l-1 1v-1m-8 8h-1l-7-1h-3l-1 2v2l3 1h1c3-1 6-2 7-4h1-1 1l-7 4-2 1-3-2-1-2 2-3a15 15 0 013 0l8 2m-10-10l-4 1-2 1-1 2h1v2l2 1c2-2 3-5 3-7h1c-1 3-2 6-4 7l-2-1-1-2 1-2c1-2 4-2 6-3v1m4-2l-3 3-1 3v2h1l3-1 2-3 1-1v-2l1-2v1h-4v-1h5l-1 1v2l-1 1-1 1-2 3-3 2a2 2 0 01-1-1 3 3 0 01-1-2l2-4 3-3v1m6 0v-1h4l-1 1-1 2h-2-1v-1-1l1-1v2l-1 1v-1h3l1-1h-3m12 1h-6-1v1l3 1 4-3v1c0 2-2 2-4 2l-3-1-1-1a1 1 0 011-1h8l-1 1m22-2v1h-3-1l-3 1v-1 1-1 2a5 5 0 002 1c2 0 4-1 4-4h1v1-1c-1 3-3 5-5 5a5 5 0 01-3-1h1-1v-1a4 4 0 010-2h1l3-1h4m-13 2v-1h5l-2 4-3 2a2 2 0 01-1-1v-1l1-4v1l-1 3 1 1h-1 1l3-2 1-3v1h-4m-3 0h-1-2l-4 8 1 3 1 1 2-2c2-2 2-8 2-10h1l-1 7-1 4-3 1-2-1-1-3c0-3 2-6 5-9h3v1m-5 23h-1l-10-1h-1l-1-1 1 1-1-1 1 1-1-1 1 1-1-1 1 1-1-1 1 1h-1v-1l1 1h-1 1-1 1-1 1-1 1l-3 1-2 3v1l3 1 6-1a2 2 0 010-1l5-1 3-2h1l-4 2-4 2h-1a2 2 0 010 1l-6 1c-1 0-2 0-3-2h-1v-1l3-3 2-1v-1h1v1l-1-1h2l10 2h1l1-1v1h-1m20-20l-6 1-6 1-2 2-2 3 1 1 2 1 6-3v1-1h1l6-6-6 6v1l-7 3a4 4 0 01-3-1v-2l2-4a18 18 0 012-1h1-1l6-2 6-1h1l-1 1m-34 28a5 5 0 01-1 0l-5-1-5-2-1 1v-1 1l-3 1-1 1-1 1 1 1 5 1h4l7-3-7 4h-1-3c-2 0-4 0-6-2l-1-1 1-1 3-2 1-1h1v1-1 1-1 1-1 1-1 1-1 1-1h1l5 1 5 2h2-1m23-17l-4 1h-8v1-1 1-1 1-1 1l-2 1-1 2v2-1l3 2 5-2 1-1 6-5-6 6-1 1-5 1-3-1-1-2 2-3a19 19 0 011-1h2-1l4-1h8l1-1-1 1m-22-2v1l-5 4c-2 2-4 3-4 5l-2 2 1 1v1-1h1l3-1 2-3h1-1 1v-1l2-8h1v1-1c0 3-1 7-3 9v-1 1l-3 4a5 5 0 01-4 1l-2-2 1-1 1-2 5-4 5-5v-1 1m9-7l-4 5-4 5-1 3v1h1l4-1 2-4v-1l2-8-1 8h-1 1v1h-1l-2 4-4 2a2 2 0 01-1-1v-1-1l1-2c0-2 2-3 4-5l4-5v-1 1m18-50v1h-2-1l-1 3 2 4h1l1-2v-2h1-1a8 8 0 000-2v-2a1 1 0 011 1v4l-1-1 1 1-1 2v1l-1 1-2-1-1-4 1-3 1-1a8 8 0 012 0m-9 17l-3 5h1l1-1 1-2-1-2h1l1 2-1 3h-1 1-2-2 1l2-5h1m3-13v2l-2 9 1 3 1 1 1-1 1-2a18 18 0 00-2-11v-1a19 19 0 012 12l-1 2-1 1h-2l1-1-1 1-1-4 3-9a2 2 0 000-1v-1m12 8l-4 3-3 1-2 2-1 1v1l4 1 2-1v1-1l1-1v-2l2-4 1-1v1l-2 4v2l-2 2h-2l-4-1a1 1 0 01-1-1l1-1a12 12 0 012-2l4-2 3-2h1m6 9h-3a2 2 0 01-1 0h-1 1-1l-1-5 2-6v-1 1l2 5 2 5v1h-1v-1h1v1-1l-2-5-2-5-1 6 1 5h1l3-1v1m-4-18h1l-5 3-4 4-1 2v2-1a5 5 0 002 0l3-1 2-3v-1c2-1 2-3 2-5h1-1 1l-2 6v1l-3 3-3 1a6 6 0 01-2 0l-1-2 1-1 1-2 4-3 4-4 1-1v2h-1m0-6v1h-1-2l-1 1-1 3v2h2l1-1 1-3 1-2v-1l1 1-1 3-2 2-1 1-1 1-1-1-1-2 1-3 2-1 2-1h1m2 2h1v2l-1 7 1 3 2 1h1l1-1 1-1-1-4-5-7h1-1c3 2 4 4 5 7l1 4v2a2 2 0 01-2 1 7 7 0 01-1 0l-3-1v-4-7-3 1m15 7c-2 3-5 6-9 8l-1 1-1 3v1h3l3-1c2-1 3-3 3-5l2-7h1l-2 7-4 5-3 2h-2-1a1 1 0 01-1-1v-1l1-3 2-1 9-8m2-13l-1 3-2 2-4 4c-2 2-3 3-3 5l1 2h1l2-2 3-2 1-2 1-1v-1a6 6 0 010-1l1-7-1 7v4l-1 1-3 3-3 2a2 2 0 01-2-1l-1-1a3 3 0 010-1c0-2 2-4 3-5l5-4 1-3 2-2m-2 0h-1-1l-1 1-1 1-1 1h1l1 1 1-1 2-2v-2l1 1-1 2v-1 1l-1 1-2 1h-2 1-1v-1l1-2a4 4 0 011-1h1l1-1v1-1h1v1m-7 3v-1h-1l-1 1v-1 1h-3-1l-1 1v-1 1-1 1-1 1-1l1 1 3 4 1 1 1-1 1-1a17 17 0 000-4h1-1v-1h1v1a16 16 0 01-1 4 4 4 0 010 2h-2-1l-4-4v-1 1a2 2 0 010-1l-1-1h5-1l2-1h2a1 1 0 011 1h-1v-1 1m-22-25h1l1 1 2 2v3l-3 2v-1l-2-6 1-1v-1l1 1h-1v1l1 4v2l3-2-1-1-2-3-1-1m16 1l2-1v-1c0-1 0-3-2-5l-2-1-2-4v1a28 28 0 000 2l1 6 3 3c-2 0-3-2-4-3v-6-3l2 3 2 1 3 6-2 2h-1m-7 2c1 0 2-1 2-4l-1-7-1-5h1l-1 1-3 11v3l2 1a5 5 0 001 0 6 6 0 01-1 0l-2-1-1-3c0-4 4-12 4-12v-1l1 1v5c2 3 2 5 2 7l-1 3-2 1m-4-12c1 0 3-1 3-4l-2-7-2-3-2-4h1a56 56 0 00-1 3l-1 8 1 5c1 1 1 2 3 2l-4-2v-5l1-12 1 1 2 4 2 3 1 7-1 3-2 1m-5-15l1-3-3-6a20 20 0 01-1-2l-3-3h1v11l2 2 1 1h2l-2 1-2-1c-2-3-2-7-2-10v-4h1l2 3 1 1h1c2 3 2 6 2 7l-1 3m-19-23h-1l1-1c0-1-1-4-7-7l-5-4 1 2 4 6c2 2 4 4 7 4h-1 1v1c-4-1-7-4-9-7l-3-6 3 2 2 1v1-1c6 4 7 6 7 8v2-1m-13-6v-2c0-2-1-4-5-9l-4-3h1v2l2 7c2 2 3 4 6 5l-5-2c-3-5-4-12-4-12l3 2a8 8 0 001 1c5 4 6 7 6 9l-1 2m36 52l1-2-4-6h1-1a42 42 0 01-2-1l-3-3h1v1l2 7 5 4c-3 0-5-3-6-6l-2-6h1l3 2 2 2c3 3 3 5 3 6l-1 2m-5-14v-1-1c0-1 0-3-4-5v-1 1l-2-1-3-2 1 1 3 5c1 2 3 3 5 3v1-1 1c-3 0-5-3-7-5a25 25 0 01-2-5l3 1a19 19 0 002 1c4 2 5 5 5 6l-1 2m-7-12h-1l1-2c0-1-1-3-6-6h-2l-4-2h1v1l4 6 6 3h1-1 1-1c-4 0-6-2-8-5l-3-5h1l3 1a21 21 0 002 1c5 2 6 5 6 6v2m-10-12l1-2c0-1-1-3-6-6h-2l-4-2h1v2l4 5 6 3h1a6 6 0 01-1 0c-4 0-6-2-8-5l-3-5h1l3 1a21 21 0 002 1c5 2 6 5 6 6v2h-1m9 3l1-3-4-7a23 23 0 01-3-1l-3-2h1v2l2 7 2 3 2 1h3l-3 1-3-2c-3-5-4-12-4-12l1-1 3 3a24 24 0 002 1c4 3 5 6 5 7l-1 3h-1m8-10h-1a2 2 0 001-1l-2-2-6-1v-1 1l-3-1h-5v-1l2 1 5 5 5 2c2 0 3 0 3-2h1c-1 2-2 3-4 3l-8-4-4-4v-1l5 1a50 50 0 003 0l7 2 1 2v1m-9-9l-2-1-7-1-8-1h2c2 2 8 6 11 6l2-1 1-2h1l-1 3h-3c-3 0-6-1-8-3a50 50 0 01-5-3v-1l5 1h3v1-1l8 1 1 2m35 34l2 11-1 6-3 3a4 4 0 01-1 0l-2-1-1-2v-3l3-6a180 180 0 002-8h1l-1 3-4 11v5h3l3-3v-5l-1-7a44 44 0 000-3l-1-1h1m-7-15s5 9 5 16c0 2-1 5-3 6l-2-1-2-6v-1l1-6 1-7v-1 1a87 87 0 01-1 13h-1 1v1l1 5 2 1v1-1l2-5-2-10a63 63 0 00-2-5v-1m-11 16h1l6 2 4 3 2 5-1 3a2 2 0 01-1 0c-1 0-4 0-7-6l-1-3-3-4v-1l1 1h-1 1l4 7c3 5 6 6 6 6h1-1l1-3-2-4c-1-2-4-3-6-4a32 32 0 00-3-1l-1-1h1-1m-6-12h1l6 2 5 3 2 5-1 2v1h-1c-1 0-4-1-7-6l-2-2-3-4v-1h1-1 1l4 7 7 5h1-1l1-2-2-4-7-4a33 33 0 00-2-1 16 16 0 00-2 0v-1h1-1m-9-11l8 1 5 2 3 4-2 4h-1c-1 0-4-1-7-4l-3-3-3-3v-1h1l5 6v1-1c3 4 6 4 7 4h1v1-1l1-3-2-3-8-3a47 47 0 00-3 0 31 31 0 00-2 0v-1h1-1m19-4s5 7 5 14c0 2 0 4-2 5v1l-2-1c-1-1-2-3-2-7v-5a142 142 0 000-7v-1l1 1v1l-1 11 2 6a4 4 0 002 1l2-5c0-4-2-7-3-9a32 32 0 00-2-3l-1-1 1-1m-11-11l4 4c2 3 4 6 4 10a9 9 0 010 4h-1a5 5 0 01-3-1c-2-1-3-3-3-5a393 393 0 00-2-12v-1l1 1a70 70 0 011 12l3 4a4 4 0 003 1v1-1a9 9 0 001-3c0-4-2-7-4-10a31 31 0 00-4-3l-1-1h1m-12-7v-1l6 3c2 2 5 5 5 10v2l-2 1c-1 0-3-1-5-5l-2-5-2-5-1-1h1v1-1l3 6 2 5h-1 1l4 4h1v-2c0-4-2-7-5-9a24 24 0 00-3-2 25 25 0 00-2-1v-1 1m-12-6l6 2c4 2 7 5 7 10v1a1 1 0 01-1 0c-2 0-3 0-5-3l-3-4-4-6-1-1 1 1 7 10 5 3v-1h1-1c0-5-3-8-6-9l-4-2-2-1m-17 3v-1h4l11 1 4 2a5 5 0 012 5v1l-3 2-4-1-2-2a512 512 0 00-7-4 146 146 0 00-3-2l-1-1a5 5 0 00-1 0v-1 1-1l1 1 14 8 3 1 2-1a3 3 0 000-1h1a4 4 0 00-2-4c-3-3-10-3-15-3h-4v-1 1"></path></g><path fill="none" stroke="#000" stroke-width=".7" d="M73 98c9 6 15 7 15 7m36-6l-8 3-16 4"></path></svg>


       
        <h1 class="text-4xl font-bold text-[#47627f] uppercase">
        O'zbekiston Respublikasi oliy sudi
        </h1>

        <p class="text-2xl text-[#8b98aa] mt-3">
         Elektron to'yxatdan o'tish tizimi
        </p>

      </div>
    </header>

    <!-- CONTAINER -->
    <div class="max-w-5xl mx-auto py-12">

      <!-- STEP INDICATOR (6 TA) -->
      <div class="flex justify-center mb-12">
        <div class="flex items-center">

          <template v-for="n in 6" :key="n">

            <div
              class="w-12 h-12 rounded-full border-2 flex items-center justify-center text-lg"
              :class="
                n <= step
                  ? 'border-blue-500 text-blue-500'
                  : 'border-gray-400 text-gray-400'
              "
            >
              {{ n }}
            </div>

            <div
              v-if="n < 6"
              class="w-9 h-[3px]"
              :class="n < step ? 'bg-blue-500' : 'bg-gray-400'"
            />


       

          </template>

        </div>
      </div>

 <!-- ================= STEP 1 ================= -->

<div
  v-if="step === 1"
  class="bg-white border rounded-lg shadow-sm"
>
  <div class="bg-gray-100 px-6 py-5">
    <h2 class="text-2xl font-bold text-[#4d5f76]">
    Shaxsiy ma'lumotlar
    </h2>
  </div>

  <h1>salom</h1>

  <div class="p-6 grid md:grid-cols-2 gap-5">


<input
type="text"
  v-model="firstName"
  placeholder="Ism"
  :class="[
    'w-full py-3 px-5 rounded-lg outline-none border',
    step1Error && firstName.trim().length < 2
      ? 'border-red-500'
      : 'border-gray-300'
  ]"
/>

<input
type="text"
  v-model="lastName"
  placeholder="Familiya"
  :class="[
    'w-full py-3 px-5 rounded-lg outline-none border',
    step1Error && lastName.trim().length < 2
      ? 'border-red-500'
      : 'border-gray-300'
  ]"
/>

<input
type="text"
  v-model="middleName"
  placeholder="Sharif"
  :class="[
    'w-full py-3 px-5 rounded-lg outline-none border',
    step1Error && middleName.trim().length < 2
      ? 'border-red-500'
      : 'border-gray-300'
  ]"
/>

<input
type="tel"
  v-model="phone"
  placeholder="+998901234567"
  :class="[
    'w-full py-3 px-5 rounded-lg outline-none border',
    step1Error && !phoneRegex.test(phone)
      ? 'border-red-500'
      : 'border-gray-300'
  ]"
/>

<input
type="email"
  v-model="email"
  placeholder="email@gmail.com"
  class="md:col-span-2"
  :class="[
    'w-full py-3 px-5 rounded-lg outline-none border',
    step1Error && !email.includes('@')
      ? 'border-red-500'
      : 'border-gray-300'
  ]"
/>

  </div>

  <div class="p-6">
    <button
      @click="nextStep()"
      class="w-full py-3 rounded bg-gray-300 hover:bg-blue-500 hover:text-white"
    >
      Keyingisi
    </button>
  </div>
</div>

<!-- ================= STEP 2 ================= -->

<div
  v-if="step === 2"
  class="bg-white border py-3 px-4 rounded-lg shadow-sm"
>

  <div class="bg-gray-100 px-6 py-5">
    <h2 class="text-2xl font-bold text-gray-700">
    Yashash manzili
    </h2>
  </div>

  <div class="p-6 grid md:grid-cols-2 gap-6">

<!-- Viloyat -->
<select
  v-model="region"
  :class="[
    'w-full py-3 px-4 rounded-lg border',
    step2Error && !region
      ? 'border-red-500'
      : 'border-gray-300'
  ]"
>
  <option value="">Viloyat tanlang</option>

  <option
    v-for="r in Object.keys(districts)"
    :key="r"
    :value="r"
  >
    {{ r }}
  </option>
</select>

<!-- Tuman -->
<select
  v-model="district"
  :class="[
    'w-full py-3 px-4 rounded-lg border',
    step2Error && !district
      ? 'border-red-500'
      : 'border-gray-300'
  ]"
>
  <option value="">Tuman tanlang</option>

  <option
    v-for="d in filteredDistricts"
    :key="d"
    :value="d"
  >
    {{ d }}
  </option>
</select>

<!-- Manzil -->
<input
  v-model="address"
  type="text"
  placeholder="To'liq manzil"
  :class="[
    'md:col-span-2 w-full py-3 px-4 rounded-lg border',
    step2Error && !address.trim()
      ? 'border-red-500'
      : 'border-gray-300'
  ]"
/>

<button
  @click="nextStep()"
  class="md:col-span-2 w-full rounded bg-gray-300 hover:bg-blue-500 py-3 hover:text-white"
>
 Keyingisi
</button>


  </div>

</div>



<!-- ================= STEP 3 ================= -->

<div
  v-if="step === 3"
  class="bg-white border py-3 px-4 rounded-lg shadow-sm"
>
  <div class="bg-gray-100 px-6 py-5">
    <h2 class="text-2xl font-bold text-gray-700">
    Kabul haqida ma'lumotlar
    </h2>
  </div>

  <div class="p-6 grid md:grid-cols-2 gap-6">


<!-- Kimning qabuliga -->
<div>
  <label class="block mb-2 font-medium">
  Kimning qabuliga yozilmoqchisz?
  </label>

  <select
    v-model="receptionType"
    :class="[
      'w-full py-3 px-4 rounded-lg border',
      step3Error && !receptionType
        ? 'border-red-500'
        : 'border-gray-300'
    ]"
  >
    <option value="">Tanlang</option>
    <option >Oliy sud Raisi</option>
    <option>Jinoyat ishlari bo'yicha rais o'rinbosari</option>
    <option>Fuqarolik ishlari bo'yicha rais o'rinbosari</option>
    <option>Ma'muriy ishlar bo'yicha raisning 1-o'rinbosari</option>
    <option>Iqtisodiy ishlar bo'yicha rais o'rinbosari</option>
  </select>
</div>

<!-- Rahbar -->
<div>
  <label class="block mb-2 font-medium">
   Raxbar F.I.Sh
  </label>

  <select
    v-model="leader"
    :class="[
      'w-full py-3 px-4 rounded-lg border',
      step3Error && !leader
        ? 'border-red-500'
        : 'border-gray-300'
    ]"
  >
    <option value="">Tanlang</option>
    <option>B. Islamov</option>
  </select>
</div>

<!-- Sud yo'nalishi -->
<div>
  <label class="block mb-2 font-medium">
    Sud yo'nalishi
  </label>

  <select
    v-model="courtDirection"
    :class="[
      'w-full py-3 px-4 rounded-lg border',
      step3Error && !courtDirection
        ? 'border-red-500'
        : 'border-gray-300'
    ]"
  >
    <option value="">Tanlang</option>
    <option>Jinoyat ishlari bo'yicha</option>
    <option>Fuqarolik ishlari bo'yicha</option>
    <option>Ma'muriy ishlari bo'yicha</option>
    <option>Iqtisodiy ishlari bo'yicha</option>
  </select>
</div>

<!-- Taraf -->
<div>
  <label class="block mb-2 font-medium">
    Ish bo'yicha taraflar
  </label>

  <select
    v-model="partyType"
    :class="[
      'w-full py-3 px-4 rounded-lg border',
      step3Error && !partyType
        ? 'border-red-500'
        : 'border-gray-300'
    ]"
  >
    <option value="">Tanlang</option>
    <option value="sudlanuvchi">Sudlanuvchi</option>
    <option value="jabrlanuvchi">Jabrlanuvchi</option>
    <option value="boshqa">Boshqa shaxs</option>
  </select>
</div>

<!-- Qo'shimcha section -->


  

<div v-if="partyType">
  <label for="">Ismi</label>
    <input
    type="text"
      v-model="caseFirstName"
      placeholder="Ismi"
      :class="[
        'w-full py-3 px-4 rounded-lg border',
        step3Error && !caseFirstName
          ? 'border-red-500'
          : 'border-gray-300'
      ]"
    />
</div>

    <div v-if="partyType">
      <label for="">Familiyasi</label>
<input
    type="text"
      v-model="caseLastName"
      placeholder="Familiyasi"
      :class="[
        'w-full py-3 px-4 rounded-lg border',
        step3Error && !caseLastName
          ? 'border-red-500'
          : 'border-gray-300'
      ]"
    />
    </div>

  <div v-if="partyType">
      <label for="">Sharifi</label>
    <input
    type="text"
      v-model="caseMiddleName"
      placeholder="Sharifi"
      :class="[
        'w-full py-3 px-4 rounded-lg border',
        step3Error && !caseMiddleName
          ? 'border-red-500'
          : 'border-gray-300'
      ]"
    />
  </div>

  

 

 <div>
   <label class="block mb-2 font-medium">
    Ish raqami
  </label>

  <input
    
      v-model="caseNumber"
      type="number"
      placeholder="Ish raqami"
      :class="[
        'w-full py-3 px-4 rounded-lg border border-gray-300',
        step3Error && !caseNumber
          ? 'border-red-500'
          : 'border-gray-300'
      ]"
    />
 </div>

<!-- Ishtirok etish -->
<div>
  <label class="block mb-2 font-medium">
    Ishtirok etish tartibi
  </label>

  <select
    v-model="participationType"
    :class="[
      'w-full py-3 px-4 rounded-lg border',
      step3Error && !participationType
        ? 'border-red-500'
        : 'border-gray-300'
    ]"
  >
    <option value="">Tanlang</option>
    <option>Videokonferensaloqa</option>
    <option>Bevosita idorada</option>
  </select>
</div>

<!-- Hudud -->
<div>
  <label class="block mb-2">
    Viloyat
  </label>

  <select
    v-model="selectedRegion"
    @change="courtRegion = ''"
    class="w-full py-3 px-4 rounded-lg border border-gray-300"
  >
    <option value="">
      Tanlang
    </option>

    <option
      v-for="region in Object.keys(districts)"
      :key="region"
      :value="region"
    >
      {{ region }}
    </option>
  </select>
</div>

<div>
  <label class="block mb-2">
    Sud
  </label>

  <select
    v-model="courtRegion"
    :disabled="!selectedRegion"
    :class="[
      'w-full py-3 px-4 rounded-lg border',
      step3Error && !courtRegion
        ? 'border-red-500'
        : 'border-gray-300'
    ]"
  >
    <option value="">
      Tanlang
    </option>

    <option
      v-for="district in districtList"
      :key="district"
      :value="district + ' тумани суди'"
    >
      {{ district }} tuman sudi
    </option>
  </select>
</div>

<!-- Sana -->
<div class="md:col-span-1">
  <label class="block mb-2 font-medium">
    Ish ko'rilgan sana
  </label>

  <input
    v-model="caseDate"
    type="date"
    :max="new Date().toISOString().split('T')[0]"
    :class="[
      'w-full py-3 px-4 rounded-lg border',
      step3Error && !caseDate
        ? 'border-red-500'
        : 'border-gray-300'
    ]"
  />
</div>

<div class="w-full flex flex-col gap-5 md:col-span-2">

  <div class="w-full bg-yellow-100 border border-yellow-400 rounded-lg p-5">
    <h2 class="text-lg font-bold text-black mb-3">
      Eslatma (*)
    </h2>

    <p class="text-black leading-7 mb-4">
   Oliy sud raisi qabuliga kirish uchun, nazorat tartibidagi shikoyatni dastlab Oliy sud sudyasi tomonidan o‘rganilib, tegishli ajrim chiqarilgan bo‘lishi va Oliy sud raisi o‘rinbosari qabulida berilgan shikoyat arizasiga Oliy sud raisi o‘rinbosari tomonidan tegishli javob xati chiqarilgan bo‘lishi lozim.</p>

  <label class="flex items-center gap-3 text-black cursor-pointer">
  <input
    type="checkbox"
    v-model="readAgreement1"
    class="w-5 h-5 accent-yellow-600"
  />
  Men o'qib chiqdim
</label>
  </div>

  <div class="w-full bg-yellow-100 border border-yellow-400 rounded-lg p-5">
    <h2 class="text-lg font-bold text-black mb-3">
      Eslatma (*)
    </h2>

    <p class="text-black leading-7 mb-4">
   O‘zbekiston Respublikasi FPKning 373-moddasiga muvofiq, ishda ishtirok etuvchi shaxslar (da’vogar, javobgar, ularning ishonchli vakillari va manfaatdor shaxslar), shuningdek ishda ishtirok etishga jalb qilinmagan, ammo huquq va majburiyatlari haqidagi masala sud tomonidan hal etilgan shaxslar sud hujjatining qonuniy, asosli va adolatli ekanligini tekshirish haqidagi shikoyat (ariza) bilan qonunda belgilangan tartibda murojaat qilishga haqli. </p>

  <label class="flex items-center gap-3 text-black cursor-pointer">
  <input
    type="checkbox"
    v-model="readAgreement2"
    class="w-5 h-5 accent-yellow-600"
  />
 Men o'qib chiqdim
</label>
  </div>

</div>


<button
  @click="nextStep()"
  class="md:col-span-2 w-full rounded bg-gray-300 hover:bg-blue-500 py-3 hover:text-white"
>
  Keyingi
</button>


  </div>
</div>




<!-- ================= STEP 4 ================= -->
<div
  v-if="step === 4"
  class="bg-white border py-3 px-4 rounded-lg shadow-sm"
>
  <div class="bg-gray-100 px-6 py-5">
    <h2 class="text-2xl font-bold text-gray-700">
      Apellyatsiya yoki kassatsiya tartibidagi ish
    </h2>
  </div>

  <div class="p-6 grid md:grid-cols-2 gap-6">

    <!-- Hudud -->
   <div>
  <label class="block mb-2 text-gray-700 font-medium">
    Xudud
  </label>

  <select
    v-model="region4"
    @change="court4 = ''"
    :class="[
      'w-full border py-3 px-4 rounded-lg',
      step4Error && !region4
        ? 'border-red-500'
        : 'border-gray-300'
    ]"
  >
    <option value="">Tanlang</option>

    <option
      v-for="region in Object.keys(districts)"
      :key="region"
      :value="region"
    >
      {{ region }}
    </option>
  </select>
</div>

    <!-- Sud -->
 <div>
  <label class="block mb-2 text-gray-700 font-medium">
    Sud
  </label>

  <select
    v-model="court4"
    :disabled="!region4"
    :class="[
      'w-full border py-3 px-4 rounded-lg',
      step4Error && !court4
        ? 'border-red-500'
        : 'border-gray-300'
    ]"
  >
    <option value="">Tanlang</option>

    <option
      v-for="court in courts4"
      :key="court"
      :value="
        court === region4
          ? `Jinoyat ishlari bo'yicha ${court} sudi`
          : `Jinoyat ishlari bo'yicha ${court} tumani sudi`
      "
    >
      {{
        court === region4
          ? `Jinoyat ishlari bo'yicha ${court} sudi`
          : `Jinoyat ishlari bo'yicha${court} tumani sudi`
      }}
    </option>
  </select>
</div>
    <!-- Ajrim sanasi -->
    <div class="md:col-span-2">
      <label class="block mb-2 text-gray-700 font-medium">
        Ajrim sanasi
      </label>

      <input
        v-model="decisionDate"
        type="date"
            :max="new Date().toISOString().split('T')[0]"

        :class="[
          'w-full border py-3 px-4 rounded-lg',
          step4Error && !decisionDate
            ? 'border-red-500'
            : 'border-gray-300'
        ]"
      />
    </div>

    <button
      @click="nextStep()"
      class="md:col-span-2 w-full rounded bg-gray-300 hover:bg-blue-500 py-3 hover:text-white"
    >
      Keyingi
    </button>

  </div>
</div>


<!-- ================= STEP 5 ================= -->

<div
  v-if="step === 5"
  class="bg-white border rounded-lg shadow-sm"
>
  <div class="bg-gray-100 px-6 py-5">
    <h2 class="text-2xl font-bold text-[#4d5f76]">
      Oliy sud sudyasi tomonidan chiqarilgan ajrim raqami va sanasi
    </h2>
  </div>

  <div class="p-6 grid md:grid-cols-2 gap-6">

    <!-- Ajrim raqami -->
    <div>
      <label class="block mb-2 font-medium text-gray-700">
        Ajrim raqami
      </label>

      <input
        v-model="orderNumber"
        type="number"

        placeholder="Kiriting"
        :class="[
          'w-full py-3 px-4 rounded-lg border outline-none',
          step5Error && !orderNumber
            ? 'border-red-500'
            : 'border-gray-300'
        ]"
      />
    </div>

    <!-- Ajrim sanasi -->
    <div>
      <label class="block mb-2 font-medium text-gray-700">
        Ajrim sanasi
      </label>

      <input
        v-model="orderDate"
        type="date"
            :max="new Date().toISOString().split('T')[0]"

        :class="[
          'w-full py-3 px-4 rounded-lg border outline-none',
          step5Error && !orderDate
            ? 'border-red-500'
            : 'border-gray-300'
        ]"
      />
    </div>

    <button
      @click="nextStep()"
      class="md:col-span-2 w-full py-3 rounded bg-gray-300 hover:bg-blue-500 hover:text-white transition"
    >
      Keyingi
    </button>

  </div>
</div>

<!-- ================= STEP 6 ================= -->

<div
  v-if="step === 6 && !formCompleted"
  class="bg-white border rounded-lg shadow-sm"
>
  <div class="bg-gray-100 px-6 py-5">
    <h2 class="text-2xl font-bold text-[#4d5f76]">
      Murojaatni yuborish
    </h2>
  </div>

  <div class="p-6">

    <label class="block mb-3 font-medium text-gray-700">
      Murojaatning qisqacha mazmuni
    </label>

    <textarea
      v-model="appealText"
      rows="5"
      :class="[
        'w-full border rounded-lg p-4 outline-none',
        step6Error && !appealText.trim()
          ? 'border-red-500'
          : 'border-gray-300'
      ]"
    />

    <div class="mt-8">

      <label class="block mb-3 font-medium text-gray-700">
        Hujjat yuklash
      </label>

      <input

        type="file"
        @change="handleFileUpload"
        
        class="w-full  border rounded-lg p-4"
        :class="[
          step6Error && !selectedFile
            ? 'border-red-500'
            : 'border-gray-300'
        ]"
      />

      <p
        v-if="selectedFile"
        class="mt-2 text-green-600"
      >
        {{ selectedFile.name }}
      </p>

    </div>

    <button
      @click="nextStep"
      class="w-full mt-8 py-3 rounded bg-gray-300 hover:bg-blue-500 hover:text-white"
    >
      Yakunlash
    </button>

  </div>
</div>

<!-- SUCCESS -->

<div
  v-if="formCompleted"
  class="bg-white border rounded-lg shadow-sm p-12 text-center"
>
  <div
    class="w-24 h-24 mx-auto rounded-full bg-green-100 flex items-center justify-center"
  >
    <svg
      class="w-14 h-14 text-green-600"
      fill="none"
      stroke="currentColor"
      stroke-width="3"
      viewBox="0 0 24 24"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        d="M5 13l4 4L19 7"
      />
    </svg>
  </div>

  <h2 class="text-3xl font-bold text-green-600 mt-6">
    Muvaffaqiyatli yuborildi
  </h2>

  <p class="mt-3 text-gray-600">
    Murojaatingiz qabul qilindi
  </p>
</div>

    </div>
  </div>
</template>
