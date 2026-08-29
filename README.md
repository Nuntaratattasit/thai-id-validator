/**
 * Thai National ID Validator with Lucky Messages
 * ตรวจสอบเลขบัตรประชาชนไทย + ข้อความโชคดี
 */

function validateThaiID(idNumber) {
  if (typeof idNumber !== 'string') {
    return {
      valid: false,
      message: '❌ กรุณากรอกเป็นข้อความ'
    };
  }

  const cleaned = idNumber.replace(/\D/g, '');

  if (cleaned.length !== 13) {
    return {
      valid: false,
      message: '❌ ต้องมี 13 หลักเท่านั้น'
    };
  }

  const digits = cleaned.split('').map(Number);

  // คำนวณ checksum ตามสูตรกรมการปกครอง
  let total = 0;
  for (let i = 0; i < 12; i++) {
    total += digits[i] * (13 - i);
  }

  const checkDigit = (11 - (total % 11)) % 10;

  if (checkDigit !== digits[12]) {
    return {
      valid: false,
      message: '❌ เลขบัตรไม่ถูกต้อง'
    };
  }

  // เลขถูกต้อง → แสดงข้อความโชคดี
  return {
    valid: true,
    message: '✅ เลขบัตรถูกต้อง',
    wealth: '💰 ความรวย — เงินทองไหลมาเทมา ร่ำรวยมั่นคง',
    luck: '🍀 ความโชคดี — โชคลาภเข้าข้างตลอดทาง',
    destiny: '✨ ดวงเด่น — ดวงชะตาเปิด เด่นทุกด้าน',
    love: '♥️ ความรัก — พบเจอคนที่ใช่ ความรักสมหวัง'
  };
}

// ---------------------- ตัวอย่างการใช้งาน ----------------------
if (typeof module !== 'undefined' && module.exports) {
  module.exports = { validateThaiID };
}

// รันทดสอบเมื่อเปิดไฟล์นี้โดยตรง
const testCases = [
  '1200100090237',
  '1-2001-00090-23-7',
  '1234567890123'
];

console.log('Thai National ID Validator with Lucky Messages');
console.log('='.repeat(55));

testCases.forEach(tid => {
  const result = validateThaiID(tid);
  console.log(`เลข: ${tid}`);

  if (result.valid) {
    console.log(result.message);
    console.log(result.wealth);
    console.log(result.luck);
    console.log(result.destiny);
    console.log(result.love);
  } else {
    console.log(result.message);
  }
  console.log('-'.repeat(55));
});

