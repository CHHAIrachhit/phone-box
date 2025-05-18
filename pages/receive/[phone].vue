<script setup>
import { useRouter, useRoute } from 'vue-router'

const router = useRouter()
const route = useRoute()

  const phone = useRoute().params.phone

  // Function to generate random phone number
  const generateRandomPhoneNumber = (countryCode) => {
    const countryFormats = {
      '🇺🇸': {
        format: '+1 ### ### ####',
        areaCodes: ['202', '212', '213', '310', '323', '415', '424', '510', '650', '702', '713', '714', '720', '786', '801', '802', '803', '804', '805', '806', '808', '810', '813', '814', '815', '816', '817', '818', '828', '830', '831', '832', '843', '845', '847', '848', '850', '854', '856', '857', '858', '859', '860', '862', '863', '864', '865', '870', '872', '878', '901', '903', '904', '906', '907', '908', '909', '910', '912', '913', '914', '915', '916', '917', '918', '919', '920', '925', '928', '929', '930', '931', '934', '936', '937', '938', '940', '941', '947', '949', '951', '952', '954', '956', '959', '970', '971', '972', '973', '978', '979', '980', '984', '985', '989']
      },
      '🇬🇧': {
        format: '+44 ## #### ####',
        areaCodes: ['20', '23', '24', '28', '29']
      },
      '🇨🇦': {
        format: '+1 ### ### ####',
        areaCodes: ['204', '226', '236', '249', '250', '289', '306', '343', '365', '403', '416', '418', '431', '437', '438', '450', '506', '514', '519', '548', '579', '581', '587', '604', '613', '639', '647', '705', '709', '778', '780', '782', '807', '819', '825', '867', '873', '902', '905']
      },
      '🇦🇺': {
        format: '+61 # #### ####',
        areaCodes: ['2', '3', '4', '7', '8']
      },
      '🇨🇳': {
        format: '+86 ## #### ####',
        areaCodes: ['10', '20', '21', '22', '23', '24', '25', '27', '28', '29', '31', '37', '41', '43', '45', '51', '53', '55', '57', '59', '71', '73', '75', '79', '81', '83', '85', '87', '89', '91', '93', '95', '97', '99']
      },
      '🇸��': {
        format: '+966 ## ### ####',
        areaCodes: ['11', '12', '13', '14', '16', '17', '50', '51', '52', '53', '54', '55', '56', '57', '58', '59']
      },
      '🇮🇳': {
        format: '+91 ## #### ####',
        areaCodes: ['11', '20', '22', '33', '40', '44', '79', '80', '120', '124', '129', '141', '144', '145', '160', '161', '172', '175', '180', '181', '183', '186', '224', '231', '233', '240', '241', '251', '253', '261', '265', '271', '275', '281', '285', '294', '297', '300', '301', '302', '303', '304', '305', '306', '307', '308', '309', '310', '311', '312', '313', '314', '315', '316', '317', '318', '319', '320', '321', '322', '323', '324', '325', '326', '327', '328', '329', '330', '331', '332', '333', '334', '335', '336', '337', '338', '339', '340', '341', '342', '343', '344', '345', '346', '347', '348', '349', '350', '351', '352', '353', '354', '355', '356', '357', '358', '359', '360', '361', '362', '363', '364', '365', '366', '367', '368', '369', '370', '371', '372', '373', '374', '375', '376', '377', '378', '379', '380', '381', '382', '383', '384', '385', '386', '387', '388', '389', '390', '391', '392', '393', '394', '395', '396', '397', '398', '399', '400', '401', '402', '403', '404', '405', '406', '407', '408', '409', '410', '411', '412', '413', '414', '415', '416', '417', '418', '419', '420', '421', '422', '423', '424', '425', '426', '427', '428', '429', '430', '431', '432', '433', '434', '435', '436', '437', '438', '439', '440', '441', '442', '443', '444', '445', '446', '447', '448', '449', '450', '451', '452', '453', '454', '455', '456', '457', '458', '459', '460', '461', '462', '463', '464', '465', '466', '467', '468', '469', '470', '471', '472', '473', '474', '475', '476', '477', '478', '479', '480', '481', '482', '483', '484', '485', '486', '487', '488', '489', '490', '491', '492', '493', '494', '495', '496', '497', '498', '499', '500', '501', '502', '503', '504', '505', '506', '507', '508', '509', '510', '511', '512', '513', '514', '515', '516', '517', '518', '519', '520', '521', '522', '523', '524', '525', '526', '527', '528', '529', '530', '531', '532', '533', '534', '535', '536', '537', '538', '539', '540', '541', '542', '543', '544', '545', '546', '547', '548', '549', '550', '551', '552', '553', '554', '555', '556', '557', '558', '559', '560', '561', '562', '563', '564', '565', '566', '567', '568', '569', '570', '571', '572', '573', '574', '575', '576', '577', '578', '579', '580', '581', '582', '583', '584', '585', '586', '587', '588', '589', '590', '591', '592', '593', '594', '595', '596', '597', '598', '599', '600', '601', '602', '603', '604', '605', '606', '607', '608', '609', '610', '611', '612', '613', '614', '615', '616', '617', '618', '619', '620', '621', '622', '623', '624', '625', '626', '627', '628', '629', '630', '631', '632', '633', '634', '635', '636', '637', '638', '639', '640', '641', '642', '643', '644', '645', '646', '647', '648', '649', '650', '651', '652', '653', '654', '655', '656', '657', '658', '659', '660', '661', '662', '663', '664', '665', '666', '667', '668', '669', '670', '671', '672', '673', '674', '675', '676', '677', '678', '679', '680', '681', '682', '683', '684', '685', '686', '687', '688', '689', '690', '691', '692', '693', '694', '695', '696', '697', '698', '699', '700', '701', '702', '703', '704', '705', '706', '707', '708', '709', '710', '711', '712', '713', '714', '715', '716', '717', '718', '719', '720', '721', '722', '723', '724', '725', '726', '727', '728', '729', '730', '731', '732', '733', '734', '735', '736', '737', '738', '739', '740', '741', '742', '743', '744', '745', '746', '747', '748', '749', '750', '751', '752', '753', '754', '755', '756', '757', '758', '759', '760', '761', '762', '763', '764', '765', '766', '767', '768', '769', '770', '771', '772', '773', '774', '775', '776', '777', '778', '779', '780', '781', '782', '783', '784', '785', '786', '787', '788', '789', '790', '791', '792', '793', '794', '795', '796', '797', '798', '799', '800', '801', '802', '803', '804', '805', '806', '807', '808', '809', '810', '811', '812', '813', '814', '815', '816', '817', '818', '819', '820', '821', '822', '823', '824', '825', '826', '827', '828', '829', '830', '831', '832', '833', '834', '835', '836', '837', '838', '839', '840', '841', '842', '843', '844', '845', '846', '847', '848', '849', '850', '851', '852', '853', '854', '855', '856', '857', '858', '859', '860', '861', '862', '863', '864', '865', '866', '867', '868', '869', '870', '871', '872', '873', '874', '875', '876', '877', '878', '879', '880', '881', '882', '883', '884', '885', '886', '887', '888', '889', '890', '891', '892', '893', '894', '895', '896', '897', '898', '899', '900', '901', '902', '903', '904', '905', '906', '907', '908', '909', '910', '911', '912', '913', '914', '915', '916', '917', '918', '919', '920', '921', '922', '923', '924', '925', '926', '927', '928', '929', '930', '931', '932', '933', '934', '935', '936', '937', '938', '939', '940', '941', '942', '943', '944', '945', '946', '947', '948', '949', '950', '951', '952', '953', '954', '955', '956', '957', '958', '959', '960', '961', '962', '963', '964', '965', '966', '967', '968', '969', '970', '971', '972', '973', '974', '975', '976', '977', '978', '979', '980', '981', '982', '983', '984', '985', '986', '987', '988', '989', '990', '991', '992', '993', '994', '995', '996', '997', '998', '999']
      },
      '🇮🇹': {
        format: '+39 ## #### ####',
        areaCodes: ['02', '06', '010', '011', '015', '019', '030', '031', '035', '039', '040', '041', '045', '049', '050', '051', '055', '059', '070', '071', '075', '079', '080', '081', '085', '089', '090', '091', '092', '095', '099']
      },
      '🇫🇷': {
        format: '+33 # ## ## ## ##',
        areaCodes: ['1', '2', '3', '4', '5', '6', '7', '8', '9']
      },
      '🇩🇪': {
        format: '+49 ### #### ####',
        areaCodes: ['30', '40', '69', '89', '211', '221', '231', '241', '251', '261', '271', '281', '291', '301', '311', '321', '331', '341', '351', '361', '371', '381', '391', '401', '421', '431', '441', '451', '461', '471', '481', '491', '511', '521', '531', '541', '551', '561', '571', '581', '591', '601', '611', '621', '631', '641', '651', '661', '671', '681', '691', '711', '721', '731', '741', '751', '761', '771', '781', '791', '821', '831', '841', '851', '861', '871', '881', '891', '911', '921', '931', '941', '951', '961', '971', '981', '991']
      },
      '🇧🇷': {
        format: '+55 ## #### ####',
        areaCodes: ['11', '12', '13', '14', '15', '16', '17', '18', '19', '21', '22', '24', '27', '28', '31', '32', '33', '34', '35', '37', '38', '41', '42', '43', '44', '45', '46', '47', '48', '49', '51', '53', '54', '55', '61', '62', '63', '64', '65', '66', '67', '68', '69', '71', '73', '74', '75', '77', '79', '81', '82', '83', '84', '85', '86', '87', '88', '89', '91', '92', '93', '94', '95', '96', '97', '98', '99']
      }
    }

    const country = countryFormats[countryCode]
    if (!country) return ''

    // Get random area code
    const areaCode = country.areaCodes[Math.floor(Math.random() * country.areaCodes.length)]
    
    // Generate remaining digits
    const remainingDigits = country.format
      .replace('+', '')
      .replace(/#/g, () => Math.floor(Math.random() * 10))
      .split(' ')
      .slice(1)
      .join('')

    return `+${country.format.split(' ')[0].replace('+', '')} ${areaCode} ${remainingDigits}`
  }

  // Function to generate random phone list
  const generatePhoneList = () => {
    const countries = [
      { code: '🇺🇸', name: 'United States' },
      { code: '🇬🇧', name: 'United Kingdom' },
      { code: '🇨🇦', name: 'Canada' },
      { code: '🇦🇺', name: 'Australia' },
      { code: '🇨🇳', name: 'China' },
      { code: '🇸🇦', name: 'Saudi Arabia' },
      { code: '🇮🇳', name: 'India' },
      { code: '🇮🇹', name: 'Italy' },
      { code: '🇫🇷', name: 'France' },
      { code: '🇩🇪', name: 'Germany' },
      { code: '🇧🇷', name: 'Brazil' }
    ]

    // Shuffle countries array
    const shuffledCountries = [...countries].sort(() => Math.random() - 0.5)
    
    // Take first 10 countries
    return shuffledCountries.slice(0, 10).map((country, index) => ({
      id: index + 1,
      country_code: country.code,
      country: country.name,
      number: generateRandomPhoneNumber(country.code)
    }))
  }

  const phone_list = ref(generatePhoneList())

  // Function to generate random messages
  const generateRandomMessages = () => {
    const senders = [
      'John Doe', 'Jane Smith', 'Mike Johnson', 'Sarah Williams', 'David Brown',
      'Emma Davis', 'James Wilson', 'Lisa Anderson', 'Robert Taylor', 'Mary Thomas'
    ]
    
    // Function to generate random number with specific length
    const generateRandomNumber = (length) => {
      return Math.floor(Math.random() * Math.pow(10, length)).toString().padStart(length, '0')
    }

    // Function to generate random amount
    const generateRandomAmount = () => {
      return (Math.random() * 1000).toFixed(2)
    }

    // Function to generate random date
    const generateRandomDate = () => {
      const date = new Date()
      date.setDate(date.getDate() + Math.floor(Math.random() * 30))
      return date.toLocaleDateString()
    }
    
    const messageTemplates = [
      // OTP Messages
      `Your OTP is: ${generateRandomNumber(6)}. Valid for 5 minutes.`,
      `Your verification code is: ${generateRandomNumber(6)}. Do not share with anyone.`,
      `Your login code is: ${generateRandomNumber(6)}. Expires in 10 minutes.`,
      `Your security code is: ${generateRandomNumber(6)}. Use this to verify your account.`,
      `Your authentication code is: ${generateRandomNumber(6)}. Valid for 3 minutes.`,
      
      // Marketing Messages
      '🎉 Special offer! Get 50% off on your first purchase. Use code: WELCOME50',
      '🔥 Flash sale! 24 hours only. Shop now and save up to 70%',
      '📱 New iPhone 15 Pro available for pre-order! Limited stock.',
      '💎 Exclusive deal: Buy 1 Get 1 Free on all premium products',
      '🎁 Free shipping on orders above $50. Shop now!',
      
      // Promotional Messages
      `Your order #${generateRandomNumber(5)} has been confirmed. Track your delivery here: [link]`,
      'Thank you for subscribing! Your premium membership is now active.',
      `Your account has been credited with ${generateRandomNumber(4)} reward points.`,
      `Your subscription will renew on ${generateRandomDate()}. Click here to manage.`,
      'Your loyalty program status has been upgraded to Gold!',
      
      // Service Messages
      `Your payment of $${generateRandomAmount()} was successful. Thank you for your business.`,
      `Your appointment is confirmed for tomorrow at ${Math.floor(Math.random() * 12 + 1)}:${Math.floor(Math.random() * 60).toString().padStart(2, '0')} ${Math.random() > 0.5 ? 'AM' : 'PM'}.`,
      `Your delivery is out for delivery. Expected arrival: ${Math.floor(Math.random() * 12 + 1)}-${Math.floor(Math.random() * 12 + 1)} ${Math.random() > 0.5 ? 'AM' : 'PM'}.`,
      `Your service request #${generateRandomNumber(5)} has been completed.`,
      'Your account statement is ready. View it here: [link]'
    ]

    const messages = []
    const today = new Date()
    
    for (let i = 0; i < 6; i++) {
      const randomDate = new Date(today)
      randomDate.setDate(today.getDate() - Math.floor(Math.random() * 30))
      randomDate.setHours(Math.floor(Math.random() * 24))
      randomDate.setMinutes(Math.floor(Math.random() * 60))
      
      messages.push({
        message: messageTemplates[Math.floor(Math.random() * messageTemplates.length)],
        sender: senders[Math.floor(Math.random() * senders.length)],
        time: randomDate.toLocaleString()
      })
    }
    
    // Sort messages by date (newest first)
    return messages.sort((a, b) => new Date(b.time) - new Date(a.time))
  }

  const message_list = ref(generateRandomMessages())
  
  const copyNumber = (number) =>{
    navigator.clipboard.writeText(number)
    alert('Number copied to clipboard')
  }

  const getNumber = async () =>{
    showMessage.value = false
    loading.value = true
    // wait 2 seconds
    await new Promise(resolve => setTimeout(resolve, 2000))
    loading.value = false
    showMessage.value = true
  }

  const getOtherNumber = async () =>{
    // get random number from phone_list
    const randomNumber = phone_list.value[Math.floor(Math.random() * phone_list.value.length)]
    //delay 1 second
    loading.value = true
    await new Promise(resolve => setTimeout(resolve, 1000))
    //redirect to new page
    location.href = `/receive/${randomNumber.number}`

  }

  const clickPhone = (number) =>{
    //redirect to new page
    location.href = `/receive/${number}`
  }

  const showMessage = ref(false)
  const loading = ref(false)



</script>


<template>
    <section id="numbers" class="container mx-auto px-6 py-12">

        <h2 class="text-4xl font-bold text-center text-blue-700 mb-10">Receive SMS on {{ phone }}</h2>

       <div class="grid grid-cols-12 gap-4">

        <!-- left phone list -->
        <div class="col-span-4 ">
            
            <div class="cursor-pointer bg-white rounded-sm shadow-md p-6 mb-4" v-for="phone in phone_list" :key="phone.phone" @click="clickPhone(phone.number)">
               <div class="flex items-center justify-between">
                <div class="flex items-center ">
                    <h3 class="text-xl font-semibold text-gray-800 mb-2">{{ phone.country_code }} {{ phone.country }}</h3>
                </div>
                <p class="text-gray-600">{{ phone.number }}</p>
               </div>
            </div>
        </div>
        <!-- right message list -->
        <div class="col-span-8 ">
            <!-- button get number with icon refresh -->
             <div class="flex justify-between items-center mb-4">
                <h3 class="text-xl font-semibold text-gray-800 mb-2">Message</h3>
                <div class="flex items-center gap-2">
                    <button class="cursor-pointer bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 transition-colors flex items-center gap-2" @click="getNumber">
                        <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                        </svg>
                        Update Message
                    </button>
                    <!-- btn get other number  -->
                    <button  class="cursor-pointer bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 transition-colors flex items-center gap-2" @click="getOtherNumber">
                        <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                        </svg>
                        Get Other Number
                    </button>
                </div>

                <!-- copy number -->
                <button class="cursor-pointer bg-gray-200 text-gray-500 px-4 py-2 rounded-md hover:bg-gray-300 transition-colors" @click="copyNumber(phone.number)">
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <rect x="9" y="9" width="13" height="13" rx="2" ry="2" stroke-width="2" stroke="currentColor" fill="none"/>
                        <rect x="3" y="3" width="13" height="13" rx="2" ry="2" stroke-width="2" stroke="currentColor" fill="none"/>
                    </svg>
                </button>

             </div>
           
            <div v-if="loading" class="flex justify-center items-center h-screen">
              <!-- loading -->
              <Loading :loading="loading" />
            </div>

            <div v-if="!showMessage" class="text-gray-500 text-sm">
                <p>➊ Refresh the page every couple of minutes to get new messages.</p>
                <p>➋ Be aware that anyone can see your messages for this number</p>
                <p>➌ Please do not verify important information</p>
            </div>

            <!-- message list -->
            <div v-if="showMessage" class="bg-white rounded-sm shadow-md p-6 mb-4" v-for="message in message_list" :key="message.message">
                <p class="text-gray-600 text-sm">{{ message.sender }} - {{ message.time }}</p>
                <p class="text-gray-600 text-lg">{{ message.message }}</p>
            </div>

           
        </div>
       </div>
    </section>

  
</template>

