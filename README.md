import React, { useState, useEffect, useRef } from 'react';
import { Menu, X, MapPin, Phone, Clock, ChevronRight, Star, ShoppingCart, Package, Apple, Zap, Users, Award, ArrowRight, Facebook, Instagram, Mail, Send } from 'lucide-react';

const RoyalHypermarket = () => {
  const [activeNav, setActiveNav] = useState('home');
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const [scrolled, setScrolled] = useState(false);
  const [modalOpen, setModalOpen] = useState(false);
  const [lang, setLang] = useState('en');
  const [visibleSections, setVisibleSections] = useState(new Set());

  // Scroll observer for animations
  useEffect(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            setVisibleSections(prev => new Set([...prev, entry.target.id]));
          }
        });
      },
      { threshold: 0.1 }
    );

    document.querySelectorAll('[data-animate]').forEach(el => observer.observe(el));
    return () => observer.disconnect();
  }, []);

  // Sticky nav scroll handler
  useEffect(() => {
    const handleScroll = () => setScrolled(window.scrollY > 50);
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  const content = {
    en: {
      nav: ['Home', 'Services', 'About', 'Blog', 'Contact'],
      hero: {
        title: 'Your Complete Shopping Destination',
        subtitle: 'Experience quality products, unbeatable prices, and exceptional service at Ottapalam\'s premier hypermarket',
        cta: 'Visit Us Today'
      },
      services: {
        title: 'Our Departments',
        items: [
          { icon: Apple, name: 'Fresh Produce', desc: 'Farm-fresh fruits, vegetables, and organic options' },
          { icon: Package, name: 'Grocery & Staples', desc: 'Complete range of daily essentials and packaged goods' },
          { icon: Zap, name: 'Electronics', desc: 'Latest gadgets and home appliances' },
          { icon: ShoppingCart, name: 'Household Items', desc: 'Everything for your home and lifestyle needs' }
        ]
      },
      about: {
        title: 'About Royal Hypermarket',
        mission: 'Serving the Ottapalam community with quality products and excellent service since our establishment.',
        values: ['Customer First', 'Quality Assurance', 'Best Prices', 'Community Focus']
      },
      contact: {
        title: 'Visit or Contact Us',
        formTitle: 'Send us a message',
        namePlaceholder: 'Your Name',
        emailPlaceholder: 'Email Address',
        messagePlaceholder: 'Your Message',
        submit: 'Send Message'
      }
    },
    ml: {
      nav: ['ഹോം', 'സേവനങ്ങൾ', 'ഞങ്ങളെക്കുറിച്ച്', 'ബ്ലോഗ്', 'ബന്ധപ്പെടുക'],
      hero: {
        title: 'നിങ്ങളുടെ സമ്പൂർണ്ണ ഷോപ്പിംഗ് കേന്ദ്രം',
        subtitle: 'ഓട്ടപ്പാലത്തിന്റെ പ്രമുഖ ഹൈപ്പർമാർക്കറ്റിൽ ഗുണമേന്മയുള്ള ഉൽപ്പന്നങ്ങൾ, മികച്ച വിലകൾ, അസാധാരണമായ സേവനം',
        cta: 'ഇന്ന് സന്ദർശിക്കൂ'
      },
      services: {
        title: 'ഞങ്ങളുടെ വിഭാഗങ്ങൾ',
        items: [
          { icon: Apple, name: 'ഫ്രഷ് പ്രൊഡ്യൂസ്', desc: 'പുതിയ പഴങ്ങൾ, പച്ചക്കറികൾ, ഓർഗാനിക് ഓപ്ഷനുകൾ' },
          { icon: Package, name: 'പലചരക്ക്', desc: 'ദൈനംദിന ആവശ്യങ്ങളുടെ സമ്പൂർണ്ണ ശ്രേണി' },
          { icon: Zap, name: 'ഇലക്ട്രോണിക്സ്', desc: 'ഏറ്റവും പുതിയ ഗാഡ്ജെറ്റുകളും വീട്ടുപകരണങ്ങളും' },
          { icon: ShoppingCart, name: 'വീട്ടുപകരണങ്ങൾ', desc: 'നിങ്ങളുടെ വീടിനും ജീവിതശൈലിക്കും ആവശ്യമായതെല്ലാം' }
        ]
      },
      about: {
        title: 'റോയൽ ഹൈപ്പർമാർക്കറ്റിനെക്കുറിച്ച്',
        mission: 'ഞങ്ങളുടെ സ്ഥാപനം മുതൽ ഗുണമേന്മയുള്ള ഉൽപ്പന്നങ്ങളും മികച്ച സേവനവുമായി ഓട്ടപ്പാലം സമൂഹത്തെ സേവിക്കുന്നു.',
        values: ['ഉപഭോക്താവ് ആദ്യം', 'ഗുണനിലവാര ഉറപ്പ്', 'മികച്ച വിലകൾ', 'സമൂഹ കേന്ദ്രീകൃതം']
      },
      contact: {
        title: 'ഞങ്ങളെ സന്ദർശിക്കുക അല്ലെങ്കിൽ ബന്ധപ്പെടുക',
        formTitle: 'ഒരു സന്ദേശം അയയ്ക്കുക',
        namePlaceholder: 'നിങ്ങളുടെ പേര്',
        emailPlaceholder: 'ഇമെയിൽ വിലാസം',
        messagePlaceholder: 'നിങ്ങളുടെ സന്ദേശം',
        submit: 'സന്ദേശം അയയ്ക്കുക'
      }
    }
  };

  const t = content[lang];

  // Testimonials data
  const testimonials = [
    {
      name: 'Santhosh A J',
      rating: 5,
      text: 'The store is spacious, clean, and easy to navigate. They offer a wide range of products, from fresh produce to electronics, all at great prices.',
      verified: true
    },
    {
      name: 'Unnikrishnan PS',
      rating: 5,
      text: 'It\'s a small beautiful mall which is very neat and clean! Great shopping experience with helpful staff.',
      verified: true
    },
    {
      name: 'Liju K Nair',
      rating: 4,
      text: 'Good to see improvements. Wide variety of products and convenient location near the bus stand.',
      verified: true
    },
    {
      name: 'Local Customer',
      rating: 5,
      text: 'Good atmosphere, good behaviour and less price and quality goods. Right in the heart of the city with ample parking.',
      verified: true
    }
  ];

  // Blog posts
  const blogPosts = [
    {
      title: 'Fresh Produce Selection Guide',
      excerpt: 'Learn how to choose the best fruits and vegetables for your family. Our expert tips for selecting farm-fresh produce.',
      author: 'Royal Team',
      readTime: '5 min read',
      featured: true
    },
    {
      title: 'Weekly Shopping Tips',
      excerpt: 'Save money and time with our weekly shopping strategies and special offers.',
      author: 'Royal Team',
      readTime: '3 min read'
    },
    {
      title: 'Kitchen Organization Hacks',
      excerpt: 'Maximize your kitchen space with these simple organization tips using our household products.',
      author: 'Royal Team',
      readTime: '4 min read'
    }
  ];

  const QuickInquiryModal = () => (
    <div className={`fixed inset-0 z-50 flex items-center justify-center p-4 ${modalOpen ? '' : 'hidden'}`}>
      <div className="absolute inset-0 bg-black bg-opacity-50" onClick={() => setModalOpen(false)} />
      <div className="relative bg-white rounded-lg p-6 max-w-md w-full shadow-2xl">
        <button onClick={() => setModalOpen(false)} className="absolute top-4 right-4 text-gray-400 hover:text-gray-600">
          <X size={20} />
        </button>
        <h3 className="text-xl font-bold text-gray-900 mb-4">Quick Inquiry</h3>
        <form className="space-y-4">
          <input type="text" placeholder="Name" className="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent" required />
          <input type="tel" placeholder="Phone" className="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent" required />
          <textarea placeholder="Message" rows="3" className="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent" required />
          <button type="submit" className="w-full bg-amber-500 text-white py-3 rounded-lg font-semibold hover:bg-amber-600 transition">
            Submit Inquiry
          </button>
        </form>
      </div>
    </div>
  );

  return (
    <div className="min-h-screen bg-white">
      {/* SEO Meta Tags */}
      <title>Royal Hypermarket - Ottapalam | Quality Products, Best Prices</title>
      
      {/* Sticky Navigation */}
      <nav className={`fixed w-full z-40 transition-all duration-300 ${scrolled ? 'bg-white shadow-lg' : 'bg-transparent'}`}>
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex justify-between items-center h-16">
            <div className="flex items-center space-x-2">
              <div className="w-10 h-10 bg-gradient-to-br from-amber-500 to-orange-600 rounded-lg flex items-center justify-center">
                <ShoppingCart className="text-white" size={24} />
              </div>
              <div>
                <h1 className={`font-bold text-lg ${scrolled ? 'text-gray-900' : 'text-white'}`}>Royal Hypermarket</h1>
                <p className={`text-xs ${scrolled ? 'text-gray-600' : 'text-gray-200'}`}>റോയൽ ഹൈപ്പർമാർക്കറ്റ്</p>
              </div>
            </div>
            
            <div className="hidden md:flex items-center space-x-8">
              {t.nav.map((item, i) => (
                <button key={i} onClick={() => setActiveNav(item.toLowerCase())} className={`font-medium transition ${scrolled ? 'text-gray-700 hover:text-amber-600' : 'text-white hover:text-amber-300'}`}>
                  {item}
                </button>
              ))}
              <button onClick={() => setLang(lang === 'en' ? 'ml' : 'en')} className={`px-4 py-2 rounded-lg border transition ${scrolled ? 'border-gray-300 text-gray-700 hover:border-amber-500' : 'border-white text-white hover:bg-white hover:text-gray-900'}`}>
                {lang === 'en' ? 'മലയാളം' : 'English'}
              </button>
            </div>

            <button onClick={() => setMobileMenuOpen(!mobileMenuOpen)} className="md:hidden">
              {mobileMenuOpen ? <X className={scrolled ? 'text-gray-900' : 'text-white'} /> : <Menu className={scrolled ? 'text-gray-900' : 'text-white'} />}
            </button>
          </div>
        </div>

        {/* Mobile Menu */}
        {mobileMenuOpen && (
          <div className="md:hidden bg-white shadow-lg">
            <div className="px-4 py-4 space-y-3">
              {t.nav.map((item, i) => (
                <button key={i} onClick={() => { setActiveNav(item.toLowerCase()); setMobileMenuOpen(false); }} className="block w-full text-left py-2 text-gray-700 hover:text-amber-600 font-medium">
                  {item}
                </button>
              ))}
              <button onClick={() => setLang(lang === 'en' ? 'ml' : 'en')} className="w-full py-2 px-4 border border-gray-300 rounded-lg text-gray-700">
                {lang === 'en' ? 'മലയാളം' : 'English'}
              </button>
            </div>
          </div>
        )}
      </nav>

      {/* Hero Section */}
      <section id="home" data-animate className="relative h-screen flex items-center justify-center overflow-hidden">
        <div className="absolute inset-0 bg-gradient-to-br from-blue-900 via-blue-800 to-amber-700" />
        <div className="absolute inset-0 opacity-20">
          <div className="absolute inset-0" style={{backgroundImage: 'repeating-linear-gradient(45deg, transparent, transparent 35px, rgba(255,255,255,.05) 35px, rgba(255,255,255,.05) 70px)'}} />
        </div>
        
        <div className="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
          <div className={`transition-all duration-1000 ${visibleSections.has('home') ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
            <h2 className="text-4xl md:text-6xl font-bold text-white mb-6">
              {t.hero.title}
            </h2>
            <p className="text-xl md:text-2xl text-gray-200 mb-8 max-w-3xl mx-auto">
              {t.hero.subtitle}
            </p>
            <div className="flex flex-col sm:flex-row gap-4 justify-center">
              <button onClick={() => setModalOpen(true)} className="bg-amber-500 text-white px-8 py-4 rounded-lg font-semibold text-lg hover:bg-amber-600 transition transform hover:scale-105 shadow-xl">
                {t.hero.cta}
              </button>
              <a href="tel:+919698300400" className="bg-white text-blue-900 px-8 py-4 rounded-lg font-semibold text-lg hover:bg-gray-100 transition transform hover:scale-105 shadow-xl">
                <Phone className="inline mr-2" size={20} />
                Call Us
              </a>
            </div>
          </div>
        </div>
      </section>

      {/* Services Overview */}
      <section id="services" data-animate className="py-20 bg-gray-50">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className={`text-center mb-16 transition-all duration-1000 ${visibleSections.has('services') ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
            <h2 className="text-4xl font-bold text-gray-900 mb-4">{t.services.title}</h2>
            <div className="w-24 h-1 bg-amber-500 mx-auto" />
          </div>
          
          <div className="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
            {t.services.items.map((service, i) => {
              const Icon = service.icon;
              return (
                <div key={i} className={`bg-white p-6 rounded-xl shadow-lg hover:shadow-2xl transition-all duration-500 transform hover:-translate-y-2 ${visibleSections.has('services') ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`} style={{transitionDelay: `${i * 100}ms`}}>
                  <div className="w-16 h-16 bg-gradient-to-br from-amber-500 to-orange-600 rounded-lg flex items-center justify-center mb-4">
                    <Icon className="text-white" size={32} />
                  </div>
                  <h3 className="text-xl font-bold text-gray-900 mb-2">{service.name}</h3>
                  <p className="text-gray-600 mb-4">{service.desc}</p>
                  <button className="text-amber-600 font-semibold flex items-center hover:text-amber-700">
                    Learn More <ChevronRight size={16} className="ml-1" />
                  </button>
                </div>
              );
            })}
          </div>
        </div>
      </section>

      {/* Testimonials */}
      <section id="testimonials" data-animate className="py-20 bg-white">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center mb-16">
            <h2 className="text-4xl font-bold text-gray-900 mb-4">What Our Customers Say</h2>
            <div className="flex items-center justify-center gap-2 mb-2">
              <div className="flex">
                {[1,2,3,4].map(i => <Star key={i} className="text-amber-500 fill-amber-500" size={20} />)}
                <Star className="text-amber-500 fill-amber-500" size={20} style={{clipPath: 'inset(0 20% 0 0)'}} />
              </div>
              <span className="text-gray-700 font-semibold">4.1 / 5</span>
              <span className="text-gray-500">(1,619 reviews)</span>
            </div>
          </div>

          <div className="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
            {testimonials.map((review, i) => (
              <div key={i} className="bg-gray-50 p-6 rounded-xl shadow-md hover:shadow-lg transition">
                <div className="flex items-center justify-between mb-4">
                  <div className="flex">
                    {[...Array(5)].map((_, j) => (
                      <Star key={j} className={`${j < review.rating ? 'text-amber-500 fill-amber-500' : 'text-gray-300'}`} size={16} />
                    ))}
                  </div>
                  {review.verified && <Award className="text-blue-500" size={16} />}
                </div>
                <p className="text-gray-700 mb-4 line-clamp-3">{review.text}</p>
                <p className="font-semibold text-gray-900">{review.name}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* About Snapshot */}
      <section id="about" data-animate className="py-20 bg-gradient-to-br from-blue-900 to-blue-800 text-white">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="grid md:grid-cols-2 gap-12 items-center">
            <div className={`transition-all duration-1000 ${visibleSections.has('about') ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-10'}`}>
              <h2 className="text-4xl font-bold mb-6">{t.about.title}</h2>
              <p className="text-xl text-gray-200 mb-8">{t.about.mission}</p>
              <div className="grid grid-cols-2 gap-4">
                {t.about.values.map((value, i) => (
                  <div key={i} className="flex items-center space-x-2">
                    <Award className="text-amber-500" size={20} />
                    <span className="font-semibold">{value}</span>
                  </div>
                ))}
              </div>
              <button className="mt-8 bg-amber-500 text-white px-6 py-3 rounded-lg font-semibold hover:bg-amber-600 transition flex items-center">
                Learn More About Us <ArrowRight className="ml-2" size={20} />
              </button>
            </div>
            
            <div className={`transition-all duration-1000 delay-300 ${visibleSections.has('about') ? 'opacity-100 translate-x-0' : 'opacity-0 translate-x-10'}`}>
              <div className="bg-white bg-opacity-10 backdrop-blur-lg rounded-2xl p-8 space-y-6">
                <div className="flex items-center space-x-4">
                  <Users className="text-amber-500" size={40} />
                  <div>
                    <p className="text-3xl font-bold">1,619+</p>
                    <p className="text-gray-300">Happy Customers</p>
                  </div>
                </div>
                <div className="flex items-center space-x-4">
                  <Package className="text-amber-500" size={40} />
                  <div>
                    <p className="text-3xl font-bold">5,000+</p>
                    <p className="text-gray-300">Products Available</p>
                  </div>
                </div>
                <div className="flex items-center space-x-4">
                  <Award className="text-amber-500" size={40} />
                  <div>
                    <p className="text-3xl font-bold">4.1/5</p>
                    <p className="text-gray-300">Customer Rating</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Blog/Insights */}
      <section id="blog" data-animate className="py-20 bg-gray-50">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center mb-16">
            <h2 className="text-4xl font-bold text-gray-900 mb-4">Shopping Tips & Insights</h2>
            <div className="w-24 h-1 bg-amber-500 mx-auto" />
          </div>

          <div className="grid lg:grid-cols-2 gap-8 mb-8">
            <div className="bg-white rounded-2xl shadow-xl overflow-hidden lg:col-span-2">
              <div className="md:flex">
                <div className="md:w-1/2 bg-gradient-to-br from-amber-500 to-orange-600 p-12 flex items-center justify-center">
                  <div className="text-white">
                    <span className="text-sm font-semibold bg-white bg-opacity-20 px-3 py-1 rounded-full">Featured Post</span>
                    <h3 className="text-3xl font-bold mt-4 mb-4">{blogPosts[0].title}</h3>
                    <p className="text-gray-100 mb-6">{blogPosts[0].excerpt}</p>
                    <div className="flex items-center space-x-4 text-sm">
                      <span>{blogPosts[0].author}</span>
                      <span>•</span>
                      <span>{blogPosts[0].readTime}</span>
                    </div>
                  </div>
                </div>
                <div className="md:w-1/2 p-8 flex items-center">
                  <button className="w-full bg-amber-500 text-white py-4 rounded-lg font-semibold hover:bg-amber-600 transition">
                    Read Full Article
                  </button>
                </div>
              </div>
            </div>
          </div>

          <div className="grid md:grid-cols-2 gap-8">
            {blogPosts.slice(1).map((post, i) => (
              <div key={i} className="bg-white rounded-xl shadow-lg overflow-hidden hover:shadow-2xl transition">
                <div className="p-6">
                  <h3 className="text-2xl font-bold text-gray-900 mb-3">{post.title}</h3>
                  <p className="text-gray-600 mb-4">{post.excerpt}</p>
                  <div className="flex items-center justify-between">
                    <div className="text-sm text-gray-500">
                      <span>{post.author}</span> • <span>{post.readTime}</span>
                    </div>
                    <button className="text-amber-600 font-semibold hover:text-amber-700">Read More →</button>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Contact */}
      <section id="contact" data-animate className="py-20 bg-white">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center mb-16">
            <h2 className="text-4xl font-bold text-gray-900 mb-4">{t.contact.title}</h2>
            <div className="w-24 h-1 bg-amber-500 mx-auto" />
          </div>

          <div className="grid lg:grid-cols-2 gap-12">
            <div>
              <h3 className="text-2xl font-bold text-gray-900 mb-6">Store Information</h3>
              
              <div className="space-y-6 mb-8">
                <div className="flex items-start space-x-4">
                  <MapPin className="text-amber-500 mt-1 flex-shrink-0" size={24} />
                  <div>
                    <p className="font-semibold text-gray-900">Address</p>
                    <p className="text-gray-600">Palat Rd, JN, Ottapalam</p>
                    <p className="text-gray-600">Kerala 679101</p>
                  </div>
                </div>
                
                <div className="flex items-start space-x-4">
                  <Phone className="text-amber-500 mt-1 flex-shrink-0" size={24} />
                  <div>
                    <p className="font-semibold text-gray-900">Phone</p>
                    <a href="tel:+919698300400" className="text-amber-600 hover:text-amber-700">096983 00400</a>
                  </div>
                </div>
                
                <div className="flex items-start space-x-4">
                  <Clock className="text-amber-500 mt-1 flex-shrink-0" size={24} />
                  <div>
                    <p className="font-semibold text-gray-900">Store Hours</p>
                    <p className="text-gray-600">Opens 8:30 AM Daily</p>
                  </div>
                </div>
              </div>

              <div className="bg-gray-100 p-6 rounded-xl">
                <h4 className="font-semibold text-gray-900 mb-4">Location Features</h4>
                <ul className="space-y-2 text-gray-600">
                  <li className="flex items-center"><ChevronRight className="text-amber-500 mr-2" size={16} />In-store pick-up available</li>
                  <li className="flex items-center"><ChevronRight className="text-amber-500 mr-2" size={16} />Home delivery service</li>
                  <li className="flex items-center"><ChevronRight className="text-amber-500 mr-2" size={16} />Ample parking space</li>
                  <li className="flex items-center"><ChevronRight className="text-amber-500 mr-2" size={16} />450m from Ottapalam Bus Stand</li>
                </ul>
              </div>
            </div>

            <div>
              <h3 className="text-2xl font-bold text-gray-900 mb-6">{t.contact.formTitle}</h3>
              <form className="space-y-4" onSubmit={(e) => { e.preventDefault(); alert('Message sent! We will contact you soon.'); }}>
                <div>
                  <input 
                    type="text" 
                    placeholder={t.contact.namePlaceholder}
                    className="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
                    required
                  />
                </div>
                <div>
                  <input 
                    type="email" 
                    placeholder={t.contact.emailPlaceholder}
                    className="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
                    required
                  />
                </div>
                <div>
                  <textarea 
                    placeholder={t.contact.messagePlaceholder}
                    rows="5"
                    className="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
                    required
                  />
                </div>
                <button 
                  type="submit"
                  className="w-full bg-amber-500 text-white py-4 rounded-lg font-semibold hover:bg-amber-600 transition flex items-center justify-center"
                >
                  <Send className="mr-2" size={20} />
                  {t.contact.submit}
                </button>
              </form>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-gray-900 text-white py-12">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="grid md:grid-cols-4 gap-8 mb-8">
            <div>
              <div className="flex items-center space-x-2 mb-4">
                <div className="w-10 h-10 bg-gradient-to-br from-amber-500 to-orange-600 rounded-lg flex items-center justify-center">
                  <ShoppingCart className="text-white" size={24} />
                </div>
                <div>
                  <h3 className="font-bold text-lg">Royal Hypermarket</h3>
                  <p className="text-sm text-gray-400">റോയൽ ഹൈപ്പർമാർക്കറ്റ്</p>
                </div>
              </div>
              <p className="text-gray-400 text-sm">Your trusted shopping destination in Ottapalam since our establishment.</p>
            </div>
            
            <div>
              <h4 className="font-semibold mb-4">Quick Links</h4>
              <ul className="space-y-2 text-gray-400">
                <li><a href="#home" className="hover:text-amber-500 transition">Home</a></li>
                <li><a href="#services" className="hover:text-amber-500 transition">Services</a></li>
                <li><a href="#about" className="hover:text-amber-500 transition">About Us</a></li>
                <li><a href="#contact" className="hover:text-amber-500 transition">Contact</a></li>
              </ul>
            </div>
            
            <div>
              <h4 className="font-semibold mb-4">Our Departments</h4>
              <ul className="space-y-2 text-gray-400">
                <li>Fresh Produce</li>
                <li>Grocery & Staples</li>
                <li>Electronics</li>
                <li>Household Items</li>
              </ul>
            </div>
            
            <div>
              <h4 className="font-semibold mb-4">Connect With Us</h4>
              <div className="flex space-x-4 mb-4">
                <a href="#" className="w-10 h-10 bg-gray-800 rounded-lg flex items-center justify-center hover:bg-amber-500 transition">
                  <Facebook size={20} />
                </a>
                <a href="#" className="w-10 h-10 bg-gray-800 rounded-lg flex items-center justify-center hover:bg-amber-500 transition">
                  <Instagram size={20} />
                </a>
                <a href="mailto:info@royalhypermarket.com" className="w-10 h-10 bg-gray-800 rounded-lg flex items-center justify-center hover:bg-amber-500 transition">
                  <Mail size={20} />
                </a>
              </div>
              <p className="text-gray-400 text-sm">Palat Rd, Ottapalam<br />Kerala 679101</p>
            </div>
          </div>
          
          <div className="border-t border-gray-800 pt-8 text-center text-gray-400 text-sm">
            <p>&copy; 2026 Royal Hypermarket. All rights reserved. | Rating: 4.1/5 (1,619 reviews)</p>
          </div>
        </div>
      </footer>

      {/* Quick Inquiry Modal */}
      <QuickInquiryModal />
    </div>
  );
};

export default RoyalHypermarket
