# claude_code_cybernetWebsite
import React, { useState } from 'react';

export default function ISPLandingPage() {
  const [activePage, setActivePage] = useState('home');
  const [showSuccess, setShowSuccess] = useState(false);
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    phone: '',
    address: '',
    plan: '',
    message: ''
  });

  const goToHome = () => {
    setActivePage('home');
    window.scrollTo(0, 0);
  };

  const goToContact = () => {
    setActivePage('contact');
    window.scrollTo(0, 0);
  };

  const choosePlan = (planName) => {
    setFormData({...formData, plan: planName});
    goToContact();
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Form Data:', formData);
    setShowSuccess(true);
    setFormData({
      name: '',
      email: '',
      phone: '',
      address: '',
      plan: '',
      message: ''
    });
    setTimeout(() => setShowSuccess(false), 5000);
  };

  const handleChange = (e) => {
    setFormData({...formData, [e.target.name]: e.target.value});
  };

  return (
    <div className="min-h-screen bg-white">
      <header className="bg-indigo-500 text-white">
        <nav className="max-w-7xl mx-auto px-6 py-5 flex justify-between items-center">
          <div className="text-2xl font-bold">CyberNet Solutions</div>
          <div className="space-x-6">
            <button onClick={goToHome} className="hover:bg-white/10 px-4 py-2 rounded">Home</button>
            <button onClick={goToContact} className="hover:bg-white/10 px-4 py-2 rounded">Contact Us</button>
          </div>
        </nav>
      </header>

      {activePage === 'home' && (
        <div>
          <div className="bg-gradient-to-br from-indigo-500 to-purple-600 text-white text-center py-20 px-6">
            <h1 className="text-5xl font-bold mb-5">Lightning Fast Internet</h1>
            <p className="text-xl mb-8">Experience speeds up to 150 Mbps with unlimited data</p>
            <button onClick={goToContact} className="bg-white text-indigo-500 px-10 py-4 rounded-lg text-lg font-bold hover:bg-gray-100">
              Get Connected Now
            </button>
          </div>

          <div className="max-w-7xl mx-auto px-6 py-16 grid md:grid-cols-3 gap-8">
            <div className="text-center p-8 bg-white rounded-xl shadow-lg">
              <div className="text-5xl mb-4">⚡</div>
              <h3 className="text-xl font-bold text-indigo-500 mb-3">Ultra-Fast Speed</h3>
              <p className="text-gray-600">Blazing fast speeds up to 150 Mbps for streaming, gaming, and more</p>
            </div>
            <div className="text-center p-8 bg-white rounded-xl shadow-lg">
              <div className="text-5xl mb-4">🔒</div>
              <h3 className="text-xl font-bold text-indigo-500 mb-3">Secure Connection</h3>
              <p className="text-gray-600">Advanced security protocols keep your data safe and protected</p>
            </div>
            <div className="text-center p-8 bg-white rounded-xl shadow-lg">
              <div className="text-5xl mb-4">🎧</div>
              <h3 className="text-xl font-bold text-indigo-500 mb-3">24/7 Support</h3>
              <p className="text-gray-600">Our support team is always ready to assist you anytime</p>
            </div>
          </div>

          <div className="bg-gray-50 py-16 px-6">
            <h2 className="text-4xl font-bold text-center mb-10">Choose Your Perfect Plan</h2>
            <div className="max-w-7xl mx-auto grid md:grid-cols-4 gap-6">
              {[
                {name: 'Fiber Basic', price: '₹499', speed: '50 Mbps'},
                {name: 'Standard', price: '₹799', speed: '75 Mbps'},
                {name: 'Premium', price: '₹999', speed: '100 Mbps'},
                {name: 'Ultra', price: '₹1499', speed: '150 Mbps'}
              ].map((plan) => (
                <div key={plan.name} className="bg-white p-8 rounded-xl shadow-lg text-center">
                  <h3 className="text-2xl font-bold text-indigo-500 mb-3">{plan.name}</h3>
                  <div className="text-3xl font-bold my-4">{plan.price}/mo</div>
                  <ul className="text-left space-y-3 mb-6">
                    <li className="border-b pb-2">{plan.speed} Speed</li>
                    <li className="border-b pb-2">Unlimited Data</li>
                    <li className="border-b pb-2">Free Router</li>
                    <li className="pb-2">24/7 Support</li>
                  </ul>
                  <button onClick={() => choosePlan(plan.name)} className="bg-white text-indigo-500 border-2 border-indigo-500 px-8 py-3 rounded-lg font-bold hover:bg-indigo-50 w-full">
                    Select
                  </button>
                </div>
              ))}
            </div>
          </div>
        </div>
      )}

      {activePage === 'contact' && (
        <div className="max-w-3xl mx-auto px-6 py-16">
          <h1 className="text-4xl font-bold text-center text-indigo-500 mb-3">Contact Us</h1>
          <p className="text-center text-gray-600 mb-10">Fill out the form and we'll get back to you within 24 hours</p>
          
          {showSuccess && (
            <div className="bg-green-500 text-white p-4 rounded-lg text-center mb-6">
              Thank you! We'll contact you soon.
            </div>
          )}

          <form onSubmit={handleSubmit} className="space-y-6">
            <div>
              <label className="block font-bold mb-2">Full Name *</label>
              <input type="text" name="name" value={formData.name} onChange={handleChange} required className="w-full p-3 border-2 border-gray-300 rounded-lg" />
            </div>

            <div>
              <label className="block font-bold mb-2">Email Address *</label>
              <input type="email" name="email" value={formData.email} onChange={handleChange} required className="w-full p-3 border-2 border-gray-300 rounded-lg" />
            </div>

            <div>
              <label className="block font-bold mb-2">Phone Number *</label>
              <input type="tel" name="phone" value={formData.phone} onChange={handleChange} required className="w-full p-3 border-2 border-gray-300 rounded-lg" />
            </div>

            <div>
              <label className="block font-bold mb-2">Installation Address *</label>
              <textarea name="address" value={formData.address} onChange={handleChange} required className="w-full p-3 border-2 border-gray-300 rounded-lg min-h-24" />
            </div>

            <div>
              <label className="block font-bold mb-2">Preferred Plan</label>
              <select name="plan" value={formData.plan} onChange={handleChange} className="w-full p-3 border-2 border-gray-300 rounded-lg">
                <option value="">Select a plan (optional)</option>
                <option value="Fiber Basic">Fiber Basic - 50 Mbps - ₹499/mo</option>
                <option value="Standard">Standard - 75 Mbps - ₹799/mo</option>
                <option value="Premium">Premium - 100 Mbps - ₹999/mo</option>
                <option value="Ultra">Ultra - 150 Mbps - ₹1499/mo</option>
              </select>
            </div>

            <div>
              <label className="block font-bold mb-2">Additional Comments</label>
              <textarea name="message" value={formData.message} onChange={handleChange} className="w-full p-3 border-2 border-gray-300 rounded-lg min-h-24" />
            </div>

            <button type="submit" className="w-full bg-gradient-to-r from-indigo-500 to-purple-600 text-white py-4 rounded-lg text-lg font-bold hover:opacity-90">
              Submit Request
            </button>
          </form>
        </div>
      )}

      <footer className="bg-gray-800 text-white text-center py-8 mt-16">
        <p>&copy; 2025 CyberNet Solutions. All rights reserved.</p>
        <p className="mt-2">Providing fast and reliable internet service</p>
      </footer>
    </div>
  );
}
