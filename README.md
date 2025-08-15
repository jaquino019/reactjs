<table className="w-full text-white border-collapse text-xs sm:text-sm">
  <thead>
    <tr className="bg-purple-800 bg-opacity-50">
      <th className="border border-purple-600 px-1 sm:px-2 py-1 sm:py-2">CID</th>
      <th className="border border-purple-600 px-1 sm:px-2 py-1 sm:py-2">Full Name</th>
      <th className="border border-purple-600 px-1 sm:px-2 py-1 sm:py-2">Email Address</th>
      <th className="border border-purple-600 px-1 sm:px-2 py-1 sm:py-2">Contact No.</th>
      <th className="border border-purple-600 px-1 sm:px-2 py-1 sm:py-2">Location</th>
      <th className="border border-purple-600 px-1 sm:px-2 py-1 sm:py-2">Date Created</th>
      <th className="border border-purple-600 px-1 sm:px-2 py-1 sm:py-2">Actions</th>
    </tr>
  </thead>
  <tbody>
    {contacts.map((contact) => (
      <tr key={contact.id} className="border-b border-white/30 hover:bg-white/20">
        <td className="px-1 sm:px-2 py-1 sm:py-2">{contact.cid}</td>
        <td className="px-1 sm:px-2 py-1 sm:py-2">{contact.fullName}</td>
        <td className="px-1 sm:px-2 py-1 sm:py-2">{contact.email}</td>
        <td className="px-1 sm:px-2 py-1 sm:py-2">{contact.contactNumber}</td>
        <td className="px-1 sm:px-2 py-1 sm:py-2">{contact.location}</td>
        <td className="px-1 sm:px-2 py-1 sm:py-2">{contact.registeredDate}</td>
        <td className="px-1 sm:px-2 py-1 sm:py-2 flex gap-1 flex-wrap">
          <button className="bg-blue-500 hover:bg-blue-600 text-white px-1 sm:px-2 py-0.5 sm:py-1 rounded text-[10px] sm:text-xs">
            View
          </button>
          <button className="bg-yellow-500 hover:bg-yellow-600 text-white px-1 sm:px-2 py-0.5 sm:py-1 rounded text-[10px] sm:text-xs">
            Update
          </button>
          <button className="bg-red-500 hover:bg-red-600 text-white px-1 sm:px-2 py-0.5 sm:py-1 rounded text-[10px] sm:text-xs">
            Delete
          </button>
        </td>
      </tr>
    ))}
  </tbody>
</table>
