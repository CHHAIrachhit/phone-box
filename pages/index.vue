<script setup>
import { ref } from 'vue'

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
    '🇸🇦': {
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

const clickPhone = (number) => {
  //redirect to new page
  location.href = `/receive/${number}`
}

const copyNumber = (number) => {
  navigator.clipboard.writeText(number)
  alert('Number copied to clipboard')
}

const refreshNumbers = () => {
  phone_list.value = generatePhoneList()
}
</script>

<template>
  <section class="container mx-auto px-6 pt-12">
    <div class="text-center mb-12">
      <h1 class="text-5xl font-bold text-blue-700 mb-4">Receive SMS Online</h1>
      <p class="text-gray-600 text-lg">Get a temporary phone number to receive SMS messages online</p>
    </div>

    <div class="flex justify-between items-center mb-8">
      <h2 class="text-2xl font-semibold text-gray-800">Available Numbers</h2>
      <button 
        @click="refreshNumbers"
        class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 transition-colors flex items-center gap-2"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
        </svg>
        Refresh Numbers
      </button>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <div 
        v-for="phone in phone_list" 
        :key="phone.id"
        class="bg-white rounded-lg shadow-md p-6 hover:shadow-lg transition-shadow cursor-pointer"
        @click="clickPhone(phone.number)"
      >
        <div class="flex items-center justify-between mb-4">
          <div class="flex items-center gap-3">
            <span class="text-2xl">{{ phone.country_code }}</span>
            <h3 class="text-xl font-semibold text-gray-800">{{ phone.country }}</h3>
          </div>
          <button 
            @click.stop="copyNumber(phone.number)"
            class="text-gray-500 hover:text-gray-700"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <rect x="9" y="9" width="13" height="13" rx="2" ry="2" stroke-width="2" stroke="currentColor" fill="none"/>
              <rect x="3" y="3" width="13" height="13" rx="2" ry="2" stroke-width="2" stroke="currentColor" fill="none"/>
            </svg>
          </button>
        </div>
        <p class="text-gray-600 text-lg">{{ phone.number }}</p>
      </div>
    </div>

    <div class="mt-12 bg-gray-50 rounded-lg p-6 ">
      <h3 class="text-xl font-semibold text-gray-800 mb-4">How it works</h3>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div class="text-center">
          <div class="bg-blue-100 rounded-full w-12 h-12 flex items-center justify-center mx-auto mb-4">
            <span class="text-blue-600 text-xl font-bold">1</span>
          </div>
          <h4 class="font-semibold mb-2">Choose a Number</h4>
          <p class="text-gray-600">Select a temporary phone number from our available list</p>
        </div>
        <div class="text-center">
          <div class="bg-blue-100 rounded-full w-12 h-12 flex items-center justify-center mx-auto mb-4">
            <span class="text-blue-600 text-xl font-bold">2</span>
          </div>
          <h4 class="font-semibold mb-2">Receive Messages</h4>
          <p class="text-gray-600">Get SMS messages sent to your chosen number</p>
        </div>
        <div class="text-center">
          <div class="bg-blue-100 rounded-full w-12 h-12 flex items-center justify-center mx-auto mb-4">
            <span class="text-blue-600 text-xl font-bold">3</span>
          </div>
          <h4 class="font-semibold mb-2">View Messages</h4>
          <p class="text-gray-600">Read and manage your received messages online</p>
        </div>
      </div>
    </div>

    <!-- About Section -->
    <div class="mt-12">
      <div class="text-center mb-8">
        <h2 class="text-3xl font-bold text-blue-700">About Our Service</h2>
        <p class="text-gray-600 mt-2">Your trusted platform for temporary SMS verification</p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-12">
        <!-- Mission -->
        <div class="bg-white rounded-lg shadow-md p-6">
          <div class="flex items-center gap-3 ">
            <div class="bg-blue-100 p-3 rounded-full">
              <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
              </svg>
            </div>
            <h3 class="text-xl font-semibold text-gray-800">Our Mission</h3>
          </div>
          <p class="text-gray-600">
            We provide a secure and reliable platform for receiving SMS messages online. Our service helps users maintain their privacy while accessing various online services that require phone verification.
          </p>
        </div>

        <!-- Features -->
        <div class="bg-white rounded-lg shadow-md p-6 mb-12">
          <div class="flex items-center gap-3 mb-4">
            <div class="bg-blue-100 p-3 rounded-full">
              <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
              </svg>
            </div>
            <h3 class="text-xl font-semibold text-gray-800">Key Features</h3>
          </div>
          <ul class="text-gray-600 space-y-2">
            <li class="flex items-center gap-2">
              <svg class="w-5 h-5 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
              </svg>
              Instant access to temporary phone numbers
            </li>
            <li class="flex items-center gap-2">
              <svg class="w-5 h-5 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
              </svg>
              Support for multiple countries
            </li>
            <li class="flex items-center gap-2">
              <svg class="w-5 h-5 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
              </svg>
              Real-time message delivery
            </li>
            <li class="flex items-center gap-2">
              <svg class="w-5 h-5 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
              </svg>
              No registration required
            </li>
          </ul>
        </div>

        <!-- Privacy -->
        <div class="bg-white rounded-lg shadow-md p-6">
          <div class="flex items-center gap-3 mb-4">
            <div class="bg-blue-100 p-3 rounded-full">
              <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
              </svg>
            </div>
            <h3 class="text-xl font-semibold text-gray-800">Privacy & Security</h3>
          </div>
          <p class="text-gray-600">
            We take your privacy seriously. Our service is designed to protect your personal information while providing a convenient way to receive SMS messages. All messages are automatically deleted after a short period for enhanced security.
          </p>
        </div>

        <!-- Support -->
        <div class="bg-white rounded-lg shadow-md p-6">
          <div class="flex items-center gap-3 mb-4">
            <div class="bg-blue-100 p-3 rounded-full">
              <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18.364 5.636l-3.536 3.536m0 5.656l3.536 3.536M9.172 9.172L5.636 5.636m3.536 9.192l-3.536 3.536M21 12a9 9 0 11-18 0 9 9 0 0118 0zm-5 0a4 4 0 11-8 0 4 4 0 018 0z" />
              </svg>
            </div>
            <h3 class="text-xl font-semibold text-gray-800">24/7 Support</h3>
          </div>
          <p class="text-gray-600">
            Our dedicated support team is available around the clock to assist you with any questions or issues you may encounter. We're committed to providing the best possible service to our users.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

