import React, { useState } from "react";

const thaiFoods = [
  "ผัดไทย",
  "ต้มยำกุ้ง",
  "แกงเขียวหวาน",
  "ข้าวมันไก่",
  "หมูกรอบผัดพริกแกง",
  "ส้มตำไทย",
  "ข้าวผัดกะเพรา",
  "ขนมจีนแกงไก่",
  "แกงมัสมั่นเนื้อ",
  "ไข่เจียวหมูสับ",
];

export default function ThaiFoodMenuApp() {
  const [selected, setSelected] = useState([]);
  const [filter, setFilter] = useState("");

  const toggleSelect = (food) => {
    setSelected((prev) =>
      prev.includes(food)
        ? prev.filter((item) => item !== food)
        : [...prev, food]
    );
  };

  const filteredFoods = thaiFoods.filter((food) =>
    food.toLowerCase().includes(filter.toLowerCase())
  );

  return (
    <div className="min-h-screen bg-gradient-to-r from-blue-900 to-indigo-800 text-white p-8">
      <h1 className="text-3xl font-bold mb-4">🍜 เลือกเมนูอาหารไทย</h1>

      <input
        type="text"
        placeholder="ค้นหาเมนู..."
        value={filter}
        onChange={(e) => setFilter(e.target.value)}
        className="p-2 rounded w-full mb-6 text-black"
      />

      <div className="grid grid-cols-2 md:grid-cols-3 gap-4">
        {filteredFoods.map((food, index) => (
          <button
            key={index}
            onClick={() => toggleSelect(food)}
            className={`p-4 rounded-xl shadow-md text-center text-lg font-medium transition transform hover:scale-105 ${
              selected.includes(food)
                ? "bg-green-500"
                : "bg-white text-black"
            }`}
          >
            {food}
          </button>
        ))}
      </div>

      <div className="mt-10">
        <h2 className="text-2xl font-semibold mb-2">✅ เมนูที่เลือก:</h2>
        {selected.length > 0 ? (
          <ul className="list-disc list-inside text-lg">
            {selected.map((food, idx) => (
              <li key={idx}>{food}</li>
            ))}
          </ul>
        ) : (
          <p>ยังไม่ได้เลือกเมนูใดเลย</p>
        )}
      </div>
    </div>
  );
}
