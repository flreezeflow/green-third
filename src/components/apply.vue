<template>
    <div class="">
        <form @submit.prevent="handleSubmit" class="">
            <div class="apply_div lg:w-2/5 rounded shadow-xl w-3/5 bg-white">
                <h2 v-if="applyState ==='apply'" class="text-center mt-10 text-lg lg:text-2xl">Appply here</h2>
                <div v-if="applyState ==='apply'" class="flex flex-col gap-4">
                    <div class="inputDiv mt-7">
                        <input :class="nameInput" type="text" id="name" v-model="name" @focus="eraseLabel('name')" @blur="restoreLabel('name')" :placeholder="nameLabel">
                        <p v-if="errors.name" class="text-red-500 text-sm text-center">{{ errors.name }}</p>
                    </div>

                    <div class="inputDiv">
                        <input :class="emailInput" type="text" id="email" v-model="email" @focus="eraseLabel('email')" @blur="restoreLabel('email')" :placeholder="emailLabel">
                        <p v-if="errors.email" class="text-red-500 text-sm text-center">{{ errors.email }}</p>
                    </div>

                    <div class="inputDiv">
                        <input :class="mobileInput" type="text" id="mobileNum" v-model="mobileNum" @focus="eraseLabel('mobileNum')" @blur="restoreLabel('mobileNum')" :placeholder="mobileNumLabel">
                        <p v-if="errors.mobileNum" class="text-red-500 text-sm text-center">{{ errors.mobileNum }}</p>
                    </div>

                    <div class="inputDiv">
                        <input :class="amountInput" type="text" id="amount" v-model="amount" @focus="eraseLabel('amount')" @blur="restoreLabel('amount')" :placeholder="amountLabel">
                        <p v-if="errors.amount" class="text-red-500 text-sm text-center">{{ errors.amount }}</p>
                    </div>

                    <div class="inputDiv">
                        <input :class="installmentsInput" type="text" id="installments" v-model="installments" @focus="eraseLabel('installments')" @blur="restoreLabel('installments')" :placeholder="installmentsLabel">
                        <p v-if="errors.installments" class="text-red-500 text-sm text-center">{{ errors.installments }}</p>
                    </div>

                    <div class="inputDivfile">
                        <label :for="namibianId" :class="idStyle" class="block border rounded text-center"><font-awesome-icon v-if="idStyle != 'border-red-500' || idStyle != 'border-limegreen'" :icon="['fas', 'upload']" :class="i_icon" class="text-black" /> {{ namibianIdLabel }}</label>
                        <input class="w-full h-full opacity-0 cursor-pointer" type="file" id="namibianId" @change="validateFile($event, 'namibianId')">
                        <p v-if="errors.namibianId" class="text-red-500 text-sm text-center">{{ errors.namibianId }}</p>
                    </div>

                    <div class="inputDivfile">
                        <label :for="bankStatement" :class="bankStatementStyle" class="block border rounded text-center"><font-awesome-icon :icon="['fas', 'upload']" :class="b_icon" class="text-black" /> {{ bankStatementLabel }}</label>
                        <input class="w-full h-full opacity-0 cursor-pointer" type="file" id="bankStatement" @change="validateFile($event, 'bankStatement')">
                        <p v-if="errors.bankStatement" class="text-red-500 text-sm text-center">{{ errors.bankStatement }}</p>
                    </div>

                    <div class="inputDivfile">
                        <label :for="paySlip" :class="paySlipStyle" class="block border rounded text-center"><font-awesome-icon :icon="['fas', 'upload']" :class="p_icon"  class="text-black" /> {{ paySlipLabel }}</label>
                        <input class="w-full h-full opacity-0 cursor-pointer" type="file" id="paySlip" @change="validateFile($event, 'paySlip')">
                        <p v-if="errors.paySlip" class="text-red-500 text-sm text-center">{{ errors.paySlip }}</p>
                    </div>
                    <p class="text-center font-semibold">{{applyInfo}}</p>
                    <div class="buttons">
                        <button type="submit" class="bg-limegreen text-center w-4/5 mb-3 rounded outline-none">Apply</button>
                    </div>
                </div>
                <div v-if="applyState === 'load'" class="flex-col rounded loader_div">
                    <p class="text-center mb-3">Please wait while we proccess your request...</p>
                    <div id="loader"  class="loader"></div>
                </div>
                <div v-if="applyState === 'success'" class="flex-col rounded loader_div">
                    <p class="text-3xl">😁</p>
                    <p class="text-center text-lg mb-3">Thank you for applying with Greenline Financial Solutions. We will contact you shortly</p>
                    <button class="bg-gray-300 text-center w-4/5 mb-3 rounded outline-none text-white font-semibold" @click="re_apply">...Re-apply</button>
                </div>
            </div>
        </form>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';

let applyState = ref('apply');
let i_icon = ref(); 
let b_icon = ref();
let p_icon = ref();

// Personal info
const name = ref('');
const mobileNum = ref('');
const amount = ref('');
const installments = ref('');
const email = ref('');
const namibianId = ref(null);
const bankStatement = ref(null);
const paySlip = ref(null);

// Labels
const nameLabel = ref('Full Name');
const mobileNumLabel = ref('Mobile Number');
const amountLabel = ref('Amount (N$500 - N$3000)');
const installmentsLabel = ref('Installments (1 - 5 Months)');
const emailLabel = ref('Email (optional)');
const namibianIdLabel = ref('ID');
const bankStatementLabel = ref('Bank Statement');
const paySlipLabel = ref('Pay Slip');
const applyInfo = ref('All docs must be in PDF format');

// Input classes
const nameInput = ref('input');
const emailInput = ref('input');
const mobileInput = ref('input');
const amountInput = ref('input');
const installmentsInput = ref('input');
const idStyle = ref('border-gray-300');
const bankStatementStyle = ref('border-gray-300');
const paySlipStyle = ref('border-gray-300');

const errors = ref({
    name: '',
    mobileNum: '',
    amount: '',
    installments: '',
    email: '',
    namibianId: '',
    bankStatement: '',
    paySlip: ''
});

function re_apply(){
    if(applyState.value != 'apply'){
        applyState.value = 'apply'
    }
}

const validateFile = (event, field) => {
    const file = event.target.files[0];
    const maxSizeInBytes = 2 * 1024 * 1024; // 2MB in bytes

    if (file) {
        if (file.type === "application/pdf" && file.size <= maxSizeInBytes) {
            switch (field) {
                case 'namibianId':
                    namibianId.value = file;
                    namibianIdLabel.value = file.name;
                    idStyle.value = 'border-limegreen';
                    i_icon.value = 'text-limegreen';
                    errors.value.namibianId = '';
                    break;
                case 'bankStatement':
                    bankStatement.value = file;
                    bankStatementLabel.value = file.name;
                    bankStatementStyle.value = 'border-limegreen';
                    b_icon.value = 'text-limegreen';
                    errors.value.bankStatement = '';
                    break;
                case 'paySlip':
                    paySlip.value = file;
                    paySlipLabel.value = file.name;
                    paySlipStyle.value = 'border-limegreen';
                    p_icon.value = 'text-limegreen';
                    errors.value.paySlip = '';
                    break;
            }
        } else {
            // File is not a PDF or exceeds the size limit
            let errorMessage = '';
            if (file.type !== "application/pdf") {
                errorMessage = 'Not in PDF format.';
            } else if (file.size > maxSizeInBytes) {
                errorMessage = 'File size exceeds 2MB.';
            }

            switch (field) {
                case 'namibianId':
                    namibianId.value = null;
                    namibianIdLabel.value = 'ID';
                    idStyle.value = 'border-red-500';
                    i_icon.value = 'text-red-500';
                    errors.value.namibianId = errorMessage;
                    break;
                case 'bankStatement':
                    bankStatement.value = null;
                    bankStatementLabel.value = 'Upload Bank Statement';
                    bankStatementStyle.value = 'border-red-500';
                    b_icon.value = 'text-red-500';
                    errors.value.bankStatement = errorMessage;
                    break;
                case 'paySlip':
                    paySlip.value = null;
                    paySlipLabel.value = 'Pay Slip';
                    paySlipStyle.value = 'border-red-500';
                    p_icon.value = 'text-red-500';
                    errors.value.paySlip = errorMessage;
                    break;
            }
        }
    }
};


async function handleSubmit(){
    clearErrors();
    let isValid = validateInfo();
    if (isValid) {
        applyState.value = 'load'
        let response
        try {
            const url = 'http://localhost:8000/';

            const formData = new FormData();
            formData.append('name', name.value);
            if(email.value){
                formData.append('email', email.value);
            }else{
                formData.append('email', 'default@gmail.com');
            }
            formData.append('mobileNum', mobileNum.value);
            formData.append('amount', amount.value);
            formData.append('installments', installments.value);
            formData.append('idFile', namibianId.value);
            formData.append('bankStatementFile', bankStatement.value);
            formData.append('paySlipFile', paySlip.value);

            response = await axios.post(url, formData, {
                headers: {
                    'Content-Type': 'multipart/form-data',
                },
            });

            if(response.data.message){
                applyState.value = 'success'
            }
            
            console.log(response.data.message)
        } catch (error) {
            window.alert('Error during submission please try agian and if the message persist please contact us')
            console.error('Error during submission:', error);
            applyState.value = 'apply'
        } finally{
            // applyState.value = 'success'
            console.log(applyState.value)
        }
    }
};

const clearErrors = () => {
    errors.value = {
        name: '',
        mobileNum: '',
        amount: '',
        installments: '',
        email: '',
        namibianId: '',
        bankStatement: '',
        paySlip: ''
    };
};

const validateInfo = () => {
    let isValid = true;
    if (!name.value) {
        nameInput.value = 'error';
        isValid = false;
    } else {
        nameInput.value = 'input';
    }
    if (!mobileNum.value) {
        mobileInput.value = 'error';
        isValid = false;
    } else if (!isValidMobileNum(mobileNum.value)) {
        errors.value.mobileNum = 'Invalid mobile number.';
        mobileInput.value = 'error';
        isValid = false;
    } else {
        mobileInput.value = 'input';
    }
    if (email.value && !isValidEmail(email.value)) {
        errors.value.email = 'Invalid email address.';
        emailInput.value = 'error';
        isValid = false;
    } else {
        emailInput.value = 'input';
    }
    if (!amount.value) {
        amountInput.value = 'error';
        isValid = false;
    } else if(amount.value > 3000 || amount.value < 500){
        errors.value.amount = 'Invalid loan amount';
        amountInput.value = 'error';
        isValid = false;
    }else{
        amountInput.value = 'input';
    }
    if (!installments.value) {
        installmentsInput.value = 'error';
        isValid = false;
    } else if(installments.value > 5 || installments.value < 0){
        installmentsInput.value = 'error';
        errors.value.installments = 'Invalid installment/s amount';
        isValid = false;
    }else{
        installmentsInput.value = 'input';
    }
    if (!namibianId.value) {
        idStyle.value = 'border-red-500';
        i_icon.value = 'text-red-500'
        isValid = false;
    } else {
        idStyle.value = 'border-gray-300';
        i_icon.value = ''
    }
    if (!bankStatement.value) {
        bankStatementStyle.value = 'border-red-500';
        b_icon.value = 'text-red-500'
        isValid = false;
    } else {
        bankStatementStyle.value = 'border-gray-300';
        b_icon.value = ''
    }
    if (!paySlip.value) {
        paySlipStyle.value = 'border-red-500';
        p_icon.value = 'text-red-500'
        isValid = false;
    } else {
        paySlipStyle.value = 'border-gray-300';
        p_icon = ''
    }
    return isValid;
};

const isValidMobileNum = (value) => {
    if (value.startsWith('+')) {
        value = value.substring(1);
    }
    const digits = value.replace(/\D/g, '');
    return (digits.length === 10 && digits.startsWith('081')) ||
           (digits.length === 13 && digits.startsWith('26481')) ||
           (digits.length === 10 && digits.startsWith('085')) ||
           (digits.length === 13 && digits.startsWith('26485'));
};

const isValidEmail = (value) => {
    const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return re.test(String(value).toLowerCase());
};

const eraseLabel = (field) => {
    switch(field) {
        case 'name':
            if (name.value === '') nameLabel.value = '';
            break;
        case 'mobileNum':
            if (mobileNum.value === '') mobileNumLabel.value = '';
            break;
        case 'amount':
            if (amount.value === '') amountLabel.value = '';
            break;
        case 'installments':
            if (installments.value === '') installmentsLabel.value = '';
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
        case 'amount':
            if (amount.value === '') amountLabel.value = 'Amount (N$500 - N$3000)';
            break;
        case 'installments':
            if (installments.value === '') installmentsLabel.value = 'Installments (1 - 5 Months)';
            break;
        case 'email':
            if (email.value === '') emailLabel.value = 'Email (optional)';
            break;
    }
};
</script>