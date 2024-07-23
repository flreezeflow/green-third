<template>
    <div class="shadow-lg w-full min-h-screen max-h-fit">
        <form @submit.prevent="handleSubmit" class="">
            <div class="apply_div rounded shadow-xl w-3/5 bg-white h-fit flex flex-col gap-4">
                <div class="inputDiv mt-7">
                    <label :for="name">{{ nameLabel }}</label>
                    <input type="text" id="name" v-model="name" @focus="eraseLabel('name')" @blur="restoreLabel('name')">
                    <p v-if="errors.name" class="text-red-500 text-sm text-center">{{ errors.name }}</p>
                </div>

                <div class="inputDiv">
                    <label :for="email">{{ emailLabel }}</label>
                    <input type="text" id="email" v-model="email" @focus="eraseLabel('email')" @blur="restoreLabel('email')">
                    <p v-if="errors.email" class="text-red-500 text-sm text-center">{{ errors.email }}</p>
                </div>

                <div class="inputDiv">
                    <label :for="mStatus">{{ mStatusLabel }}</label>
                    <select id="mStatus" v-model="mStatus" class="w-4/5 h-6 outline-none" @focus="eraseLabel('mStatus')" @blur="restoreLabel('mStatus')">
                        <option value="married">Married</option>
                        <option value="single">Single</option>
                        <option value="divorced">Divorced</option>
                        <option value="widowed">Widowed</option>
                    </select>
                    <p v-if="errors.mStatus" class="text-red-500 text-sm text-center">{{ errors.mStatus }}</p>
                </div>

                <div class="inputDiv">
                    <label :for="mobileNum">{{ mobileNumLabel }}</label>
                    <input type="text" id="mobileNum" v-model="mobileNum" @focus="eraseLabel('mobileNum')" @blur="restoreLabel('mobileNum')">
                    <p v-if="errors.mobileNum" class="text-red-500 text-sm text-center">{{ errors.mobileNum }}</p>
                </div>

                <div class="inputDiv">
                    <label :for="idNum">{{ idNumLabel }}</label>
                    <input type="text" id="idNum" v-model="idNum" @focus="eraseLabel('idNum')" @blur="restoreLabel('idNum')">
                    <p v-if="errors.idNum" class="text-red-500 text-sm text-center">{{ errors.idNum }}</p>
                </div>

                <div class="inputDivfile">
                    <label :for="namibianId" class="block border border-greenline cursor-pointe text-center">{{ namibianIdLabel }}</label>
                    <input class="w-full h-full opacity-0 cursor-pointer" type="file" id="namibianId" @change="validateFile($event, 'namibianId')">
                    <p v-if="errors.namibianId" class="text-red-500 text-sm text-center">{{ errors.namibianId }}</p>
                </div>

                <div class="inputDivfile">
                    <label :for="bankStatement" class="block border border-greenline cursor-pointe text-center">{{ bankStatementLabel }}</label>
                    <input class="w-full h-full opacity-0 cursor-pointer" type="file" id="bankStatement" @change="validateFile($event, 'bankStatement')">
                    <p v-if="errors.bankStatement" class="text-red-500 text-sm text-center">{{ errors.bankStatement }}</p>
                </div>

                <div class="inputDivfile">
                    <label :for="paySlip" class="block border border-greenline cursor-pointe text-center">{{ paySlipLabel }}</label>
                    <input class="w-full h-full opacity-0 cursor-pointer" type="file" id="paySlip" @change="validateFile($event, 'paySlip')">
                    <p v-if="errors.paySlip" class="text-red-500 text-sm text-center">{{ errors.paySlip }}</p>
                </div>

                <div class="buttons">
                    <button type="submit" class="bg-greenline text-center w-2/5 mb-3 rounded">Apply</button>
                </div>
            </div>
        </form>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const formState = ref('personalInfo');

// Personal info
const name = ref('');
const mobileNum = ref('');
const idNum = ref('');
const mStatus = ref('');
const email = ref('');
const namibianId = ref(null);
const bankStatement = ref(null);
const paySlip = ref(null);

// Labels
// Personal Info Labels
const nameLabel = ref('Full Name');
const mobileNumLabel = ref('Mobile Number');
const idNumLabel = ref('Id Number');
const mStatusLabel = ref('Marital Status');
const emailLabel = ref('Email');
const namibianIdLabel = ref('Upload Namibian ID');
const bankStatementLabel = ref('Bank Statement');
const paySlipLabel = ref('Upload Pay Slip');

const errors = ref({
    name: '',
    mobileNum: '',
    idNum: '',
    mStatus: '',
    email: '',
    namibianId: '',
    bankStatement: '',
    paySlip: ''
});

const handleSubmit = () => {
    clearErrors();
    let isValid = validateInfo();
    if (isValid) {
        const formData = {
            name: name.value,
            mobileNum: mobileNum.value,
            idNum: idNum.value,
            gender: gender.value,
            mStatus: mStatus.value,
            email: email.value
        };
        console.log('Form Data:', formData);
        // Add form submission logic here, e.g., API call
    }
};

const clearErrors = () => {
    errors.value = {
        name: '',
        mobileNum: '',
        idNum: '',
        gender: '',
        mStatus: '',
        email: ''
    };
};

const validateInfo = () => {
    let isValid = true;
    if (!name.value) {
        errors.value.name = `*Please fill out this field.`;
        isValid = false;
    }
    if (!mobileNum.value) {
        errors.value.mobileNum = `*Please fill out this field.`;
        isValid = false;
    } else if (!isValidMobileNum(mobileNum.value)) {
        errors.value.mobileNum = `*Please enter a valid Namibian mobile number.`;
        isValid = false;
    }
    if (!idNum.value) {
        errors.value.idNum = `*Please fill out this field.`;
        isValid = false;
    }
    if (!mStatus.value) {
        errors.value.mStatus = `*Please select a marital status.`;
        isValid = false;
    }
    if (!email.value) {
        errors.value.email = `*Please fill out this field.`;
        isValid = false;
    } else if (!isValidEmail(email.value)) {
        errors.value.email = `*Please enter a valid email address.`;
        isValid = false;
    }
    if (!namibianId.value) {
        errors.value.namibianId = `*Please upload a Namibian ID in PDF format.`;
        isValid = false;
    }
    if (!bankStatement.value) {
        errors.value.bankStatement = `*Please upload a Bank Statement in PDF format.`;
        isValid = false;
    }
    if (!paySlip.value) {
        errors.value.paySlip = `*Please upload a Pay Slip in PDF format.`;
        isValid = false;
    }
    return isValid;
};

const isValidMobileNum = (value) => {
    // Remove any leading "+"
    if (value.startsWith('+')) {
        value = value.substring(1);
    }
    // Remove all non-digit characters
    const digits = value.replace(/\D/g, '');
    // Check if the digits length is 10 or 13 and start with the specified prefixes
    return (digits.length === 10 && digits.startsWith('081')) ||
           (digits.length === 13 && digits.startsWith('26481')) ||
           (digits.length === 10 && digits.startsWith('085')) ||
           (digits.length === 13 && digits.startsWith('26485'));
};

const isValidEmail = (value) => {
    // Simple email validation regex
    const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return re.test(String(value).toLowerCase());
};

const validateFile = (event, field) => {
    const file = event.target.files[0];
    if (file && file.type === "application/pdf") {
        switch (field) {
            case 'namibianId':
                namibianId.value = file;
                namibianIdLabel.value = file.name;
                errors.value.namibianId = '';
                break;
            case 'bankStatement':
                bankStatement.value = file;
                bankStatementLabel.value = file.name;
                errors.value.bankStatement = '';
                break;
            case 'paySlip':
                paySlip.value = file;
                paySlipLabel.value = file.name;
                errors.value.paySlip = '';
                break;
        }
    } else {
        switch (field) {
            case 'namibianId':
                namibianId.value = null;
                namibianIdLabel.value = 'Upload Namibian ID';
                errors.value.namibianId = `*Please upload a Namibian ID in PDF format.`;
                break;
            case 'bankStatement':
                bankStatement.value = null;
                bankStatementLabel.value = 'Upload Bank Statement';
                errors.value.bankStatement = `*Please upload a Bank Statement in PDF format.`;
                break;
            case 'paySlip':
                paySlip.value = null;
                paySlipLabel.value = 'Upload Pay Slip';
                errors.value.paySlip = `*Please upload a Pay Slip in PDF format.`;
                break;
        }
    }
};

const eraseLabel = (field) => {
    switch(field) {
        case 'name':
            if (name.value === '') nameLabel.value = '';
            break;
        case 'mobileNum':
            if (mobileNum.value === '') mobileNumLabel.value = '';
            break;
        case 'idNum':
            if (idNum.value === '') idNumLabel.value = '';
            break;
        case 'mStatus':
            if (mStatus.value === '') mStatusLabel.value = '';
            break;
        case 'email':
            if (email.value === '') emailLabel.value = '';
            break;
    }
};

const restoreLabel = (field) => {
    switch(field) {
        case 'name':
            if (name.value === '') nameLabel.value = 'Full Name';
            break;
        case 'mobileNum':
            if (mobileNum.value === '') mobileNumLabel.value = 'Mobile Number';
            break;
        case 'idNum':
            if (idNum.value === '') idNumLabel.value = 'Id Number';
            break;
        case 'mStatus':
            if (mStatus.value === '') mStatusLabel.value = 'Marital Status';
            break;
        case 'email':
            if (email.value === '') emailLabel.value = 'Email';
            break;
    }
};

</script>
