// src/pages/DeleteContact.jsx
import React, { useEffect, useState } from "react";
import { useParams, useNavigate } from "react-router-dom";
import axios from "axios";
import Header from "../components/Header";
import Footer from "../components/Footer";

const DeleteContact = () => {
  const { id } = useParams();
  const navigate = useNavigate();
  const [contact, setContact] = useState(null);
  const [showConfirm, setShowConfirm] = useState(false);

  useEffect(() => {
    axios
      .get(`http://localhost:5001/contacts/${id}`)
      .then((res) => setContact(res.data))
      .catch((err) => console.error(err));
  }, [id]);

  const handleDeleteClick = () => {
    setShowConfirm(true);
  };

  const handleConfirmDelete = () => {
    axios
      .delete(`http://localhost:5001/contacts/${id}`)
      .then(() => navigate("/"))
      .catch((err) => console.error(err));
  };

  if (!contact) return <div className="text-white p-4">Loading...</div>;

  return (
    <div className="min-h-screen flex flex-col bg-gradient-to-r from-purple-800 via-purple-600 to-pink-500">
      <Header />
      <main className="flex-grow flex items-center justify-center p-6">
        <div className="p-6 text-white bg-white bg-opacity-10 rounded-lg shadow-lg w-full max-w-2xl mx-auto">
          <h2 className="text-xl font-bold mb-6">Delete Contact</h2>

          <div className="space-y-3 text-lg">
            <p><strong>CID:</strong> {contact.cid}</p>
            <p><strong>Full Name:</strong> {contact.fullName}</p>
            <p><strong>Email Address:</strong> {contact.email}</p>
            <p><strong>Contact No:</strong> {contact.contactNumber}</p>
            <p><strong>Location:</strong> {contact.location}</p>
            <p><strong>Date Created:</strong> {contact.registeredDate}</p>
          </div>

          <div className="mt-6">
            <p className="text-red-300 mb-4">
            </p>
            <div className="flex gap-3">
              <button
                onClick={handleDeleteClick}
                className="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-md"
              >
               Delete
              </button>
              <button
                onClick={() => navigate(-1)}
                className="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-md"
              >
                Cancel
              </button>
            </div>
          </div>
        </div>
      </main>
      <Footer />

      {/* Confirmation Modal */}
      {showConfirm && (
        <div className="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
          <div className="bg-white text-black rounded-lg p-6 max-w-lg w-full">
            <h3 className="text-lg font-bold mb-4 text-red-600">Confirm Deletion</h3>
            <p className="mb-4">
              Are you sure you want to delete <strong>{contact.fullName}</strong>?  
              This action cannot be undone.
            </p>
            <div className="flex gap-3">
              <button
                onClick={handleConfirmDelete}
                className="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-md"
              >
                Yes, Delete
              </button>
              <button
                onClick={() => setShowConfirm(false)}
                className="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-md"
              >
                Cancel
              </button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
};

export default DeleteContact;
