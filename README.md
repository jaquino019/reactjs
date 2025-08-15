
import React, { useState } from "react";
import axios from "axios";

const ContactForm = ({ onContactAdded }) => {
  const today = new Date().toISOString().split("T")[0]; // YYYY-MM-DD

  const [formData, setFormData] = useState({
    fullName: "",
    email: "",
    contactNumber: "",
    location: "",
    registeredDate: "", // Empty so placeholder shows
  });
  const [errors, setErrors] = useState({});

  const validate = () => {
    let temp = {};

    // Full Name validation
    const fullNamePattern = /^[A-Z][a-z]+, [A-Z][a-z]+ [A-Z]\.$/;
    if (!formData.fullName.trim()) {
      temp.fullName = "Full Name is required.";
    } else if (formData.fullName.length > 30) {
      temp.fullName = "Full Name must not exceed 30 characters.";
    } else if (!fullNamePattern.test(formData.fullName)) {
      temp.fullName =
        "Format must be: Surname, Firstname M.I (e.g., Aquino, Jaime R.)";
    } else {
      temp.fullName = "";
    }

    // Email validation
    temp.email = /\S+@\S+\.\S+/.test(formData.email)
      ? ""
      : "Valid Email is required.";

    // Contact Number validation
    temp.contactNumber =
      /^[0-9]{11}$/.test(formData.contactNumber) &&
      formData.contactNumber.startsWith("09")
        ? ""
        : "Contact Number must be 11 digits and start with 09.";

    // Location validation
    temp.location = formData.location ? "" : "Location is required.";

    // Registered Date validation (must be today)
    if (!formData.registeredDate) {
      temp.registeredDate = "Date is required.";
    } else if (formData.registeredDate !== today) {
      temp.registeredDate = "Date must be today's date.";
    } else {
      temp.registeredDate = "";
    }

    setErrors(temp);
    return Object.values(temp).every((x) => x === "");
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    if (!validate()) return;

    const cidDate = new Date(formData.registeredDate);
    const cid =
      cidDate
        .toLocaleDateString("en-US", {
          month: "2-digit",
          day: "2-digit",
          year: "numeric",
        })
        .replace(/\//g, "") + String(Date.now()).slice(-3);

    try {
      await axios.post("http://localhost:5001/contacts", {
        ...formData,
        cid,
      });
      setFormData({
        fullName: "",
        email: "",
        contactNumber: "",
        location: "",
        registeredDate: "",
      });
      if (onContactAdded) onContactAdded();
    } catch (error) {
      console.error("Error adding contact:", error);
    }
  };

  return (
    <form onSubmit={handleSubmit} className="space-y-4 text-white">
      {/* Full Name */}
      <div>
        <label className="block text-sm font-medium mb-1">Full Name</label>
        <input
          type="text"
          placeholder="Surname, Firstname M.I"
          value={formData.fullName}
          onChange={(e) =>
            setFormData({ ...formData, fullName: e.target.value })
          }
          maxLength={30}
          className="w-full p-2 rounded bg-white/10 text-white placeholder-gray-300"
        />
        {errors.fullName && (
          <p className="text-red-300 text-sm">{errors.fullName}</p>
        )}
      </div>

      {/* Email */}
      <div>
        <label className="block text-sm font-medium mb-1">Email Address</label>
        <input
          type="email"
          placeholder="example@email.com"
          value={formData.email}
          onChange={(e) =>
            setFormData({ ...formData, email: e.target.value })
          }
          className="w-full p-2 rounded bg-white/10 text-white placeholder-gray-300"
        />
        {errors.email && (
          <p className="text-red-300 text-sm">{errors.email}</p>
        )}
      </div>

      {/* Contact Number */}
      <div>
        <label className="block text-sm font-medium mb-1">Contact Number</label>
        <input
          type="text"
          placeholder="eg. 09123456789"
          value={formData.contactNumber}
          onChange={(e) =>
            setFormData({ ...formData, contactNumber: e.target.value })
          }
          className="w-full p-2 rounded bg-white/10 text-white placeholder-gray-300"
        />
        {errors.contactNumber && (
          <p className="text-red-300 text-sm">{errors.contactNumber}</p>
        )}
      </div>

      {/* Location */}
      <div>
        <label className="block text-sm font-medium mb-1">Location</label>
        <select
          value={formData.location}
          onChange={(e) =>
            setFormData({ ...formData, location: e.target.value })
          }
          className="w-full p-2 rounded bg-white/10 text-white"
          style={{
            backgroundColor: "rgba(255,255,255,0.15)",
            color: "white",
          }}
        >
          <option value="" className="bg-gray-800 text-white">
            Select Location
          </option>
          <option value="Manila" className="bg-gray-800 text-white">
            Manila
          </option>
          <option value="Cebu" className="bg-gray-800 text-white">
            Cebu
          </option>
        </select>
        {errors.location && (
          <p className="text-red-300 text-sm">{errors.location}</p>
        )}
      </div>

      {/* Register Date */}
      <div>
        <label className="block text-sm font-medium mb-1">
          Registered Date
        </label>
        <input
          type="date"
          value={formData.registeredDate}
          onChange={(e) =>
            setFormData({ ...formData, registeredDate: e.target.value })
          }
          min={today}
          max={today}
          className="w-full p-2 rounded bg-white/10 text-white placeholder-gray-300"
        />
        {errors.registeredDate && (
          <p className="text-red-300 text-sm">{errors.registeredDate}</p>
        )}
      </div>

      {/* Submit */}
      <button
        type="submit"
        className="w-full py-2 rounded bg-purple-600 hover:bg-purple-700 transition"
      >
        Add Contact
      </button>
    </form>
  );
};

export default ContactForm;
