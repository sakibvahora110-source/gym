# gym
import React, { useState, useEffect } from 'react';
import { 
  Dumbbell, 
  Apple, 
  Trophy, 
  Users, 
  Calendar, 
  ChevronRight, 
  Star, 
  CheckCircle2, 
  Mail, 
  Phone, 
  MapPin,
  Menu,
  X,
  HeartPulse,
  Flame,
  Utensils
} from 'lucide-react';

const App = () => {
  const [activeTab, setActiveTab] = useState('home');
  const [isMenuOpen, setIsMenuOpen] = useState(false);
  const [scrolled, setScrolled] = useState(false);

  useEffect(() => {
    const handleScroll = () => {
      setScrolled(window.scrollY > 50);
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  const navigate = (tab) => {
    setActiveTab(tab);
    setIsMenuOpen(false);
    window.scrollTo(0, 0);
  };

  // --- Components ---

  const Navbar = () => (
    <nav className={`fixed w-full z-50 transition-all duration-300 ${scrolled ? 'bg-zinc-900 shadow-xl py-2' : 'bg-transparent py-4'}`}>
      <div className="max-w-7xl mx-auto px-4 flex justify-between items-center">
        <div className="flex items-center gap-2 cursor-pointer" onClick={() => navigate('home')}>
          <div className="bg-lime-400 p-1.5 rounded-lg">
            <Dumbbell className="text-zinc-900 w-6 h-6" />
          </div>
          <span className="text-2xl font-black italic tracking-tighter text-white">IRONPULSE</span>
        </div>

        {/* Desktop Nav */}
        <div className="hidden md:flex items-center gap-8">
          {['home', 'programs', 'blog', 'pricing', 'contact'].map((item) => (
            <button
              key={item}
              onClick={() => navigate(item)}
              className={`capitalize font-medium transition-colors ${activeTab === item ? 'text-lime-400' : 'text-gray-300 hover:text-white'}`}
            >
              {item}
            </button>
          ))}
          <button 
            onClick={() => navigate('pricing')}
            className="bg-lime-400 hover:bg-lime-500 text-zinc-900 px-6 py-2 rounded-full font-bold transition-all transform hover:scale-105"
          >
            Join Now
          </button>
        </div>

        {/* Mobile Menu Toggle */}
        <button className="md:hidden text-white" onClick={() => setIsMenuOpen(!isMenuOpen)}>
          {isMenuOpen ? <X size={28} /> : <Menu size={28} />}
        </button>
      </div>

      {/* Mobile Nav Overlay */}
      {isMenuOpen && (
        <div className="md:hidden absolute top-full left-0 w-full bg-zinc-900 border-t border-zinc-800 flex flex-col p-6 gap-4 animate-in slide-in-from-top">
          {['home', 'programs', 'blog', 'pricing', 'contact'].map((item) => (
            <button
              key={item}
              onClick={() => navigate(item)}
              className={`capitalize text-left text-xl font-bold ${activeTab === item ? 'text-lime-400' : 'text-white'}`}
            >
              {item}
            </button>
          ))}
          <button className="bg-lime-400 text-zinc-900 p-4 rounded-xl font-bold mt-4">
            Join Now
          </button>
        </div>
      )}
    </nav>
  );

  const Hero = () => (
    <section className="relative h-screen flex items-center justify-center overflow-hidden">
      <div className="absolute inset-0 z-0">
        <img 
          src="https://images.unsplash.com/photo-1534438327276-14e5300c3a48?q=80&w=2070&auto=format&fit=crop" 
          alt="Gym Hero" 
          className="w-full h-full object-cover brightness-50"
        />
        <div className="absolute inset-0 bg-gradient-to-t from-zinc-950 via-transparent to-zinc-950/50" />
      </div>
      
      <div className="relative z-10 text-center px-4 max-w-4xl">
        <h2 className="text-lime-400 font-bold tracking-widest uppercase mb-4 animate-pulse">Push Your Limits</h2>
        <h1 className="text-5xl md:text-8xl font-black text-white italic tracking-tighter mb-6 leading-tight">
          EVOLVE YOUR <br /> <span className="text-transparent border-text stroke-white">STRENGTH</span>
        </h1>
        <p className="text-gray-300 text-lg md:text-xl mb-10 max-w-2xl mx-auto">
          The ultimate fitness destination. Professional coaching, state-of-the-art equipment, and a community built on grit.
        </p>
        <div className="flex flex-col sm:flex-row gap-4 justify-center">
          <button onClick={() => navigate('programs')} className="bg-lime-400 text-zinc-900 px-10 py-4 rounded-xl font-black text-lg hover:bg-lime-500 transition-all flex items-center justify-center gap-2">
            START TRAINING <ChevronRight size={20} />
          </button>
          <button onClick={() => navigate('pricing')} className="border-2 border-white text-white px-10 py-4 rounded-xl font-black text-lg hover:bg-white hover:text-zinc-900 transition-all">
            VIEW PLANS
          </button>
        </div>
      </div>
    </section>
  );

  const Stats = () => (
    <div className="bg-zinc-900 py-12 border-y border-zinc-800">
      <div className="max-w-7xl mx-auto px-4 grid grid-cols-2 md:grid-cols-4 gap-8 text-center">
        {[
          { label: 'Expert Trainers', val: '25+' },
          { label: 'Modern Equipment', val: '100+' },
          { label: 'Active Members', val: '2k+' },
          { label: 'Happy Clients', val: '98%' }
        ].map((stat, i) => (
          <div key={i}>
            <div className="text-3xl md:text-4xl font-black text-lime-400 mb-1">{stat.val}</div>
            <div className="text-gray-400 uppercase text-xs font-bold tracking-widest">{stat.label}</div>
          </div>
        ))}
      </div>
    </div>
  );

  const HomeContent = () => (
    <>
      <Hero />
      <Stats />
      
      {/* Why Choose Us */}
      <section className="py-24 bg-zinc-950 text-white">
        <div className="max-w-7xl mx-auto px-4">
          <div className="flex flex-col md:flex-row items-end justify-between mb-16 gap-6">
            <div className="max-w-2xl">
              <h3 className="text-lime-400 font-bold uppercase tracking-widest mb-2">Why IronPulse</h3>
              <h2 className="text-4xl md:text-5xl font-black italic">BEYOND THE AVERAGE WORKOUT</h2>
            </div>
            <p className="text-gray-400 max-w-sm">We provide an environment where discipline meets results. No shortcuts, just hard work.</p>
          </div>

          <div className="grid md:grid-cols-3 gap-8">
            {[
              { icon: <Dumbbell />, title: "Elite Coaching", desc: "Train with certified professionals who customize every aspect of your journey." },
              { icon: <Users />, title: "Community Focus", desc: "Join a tribe of motivated individuals who push each other to the next level." },
              { icon: <Calendar />, title: "24/7 Access", desc: "Your schedule, your rules. Access our facilities whenever you need your fix." }
            ].map((feature, idx) => (
              <div key={idx} className="bg-zinc-900 p-8 rounded-3xl border border-zinc-800 hover:border-lime-400/50 transition-all group">
                <div className="text-lime-400 mb-6 transform group-hover:scale-110 transition-transform">
                  {React.cloneElement(feature.icon, { size: 40 })}
                </div>
                <h4 className="text-xl font-bold mb-4 italic uppercase">{feature.title}</h4>
                <p className="text-gray-400 leading-relaxed">{feature.desc}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Trainers Preview */}
      <section className="py-24 bg-zinc-900">
        <div className="max-w-7xl mx-auto px-4 text-center mb-16">
          <h2 className="text-4xl font-black italic mb-4">OUR ELITE SQUAD</h2>
          <div className="w-24 h-1 bg-lime-400 mx-auto" />
        </div>
        <div className="max-w-7xl mx-auto px-4 grid md:grid-cols-3 gap-10">
          {[
            { name: "Marcus 'Tank' Stone", role: "Strength Specialist", img: "https://images.unsplash.com/photo-1567013127542-490d757e51fc?q=80&w=1974&auto=format&fit=crop" },
            { name: "Sarah Jenkins", role: "HIIT & Cardio Expert", img: "https://images.unsplash.com/photo-1518310383802-640c2de311b2?q=80&w=2070&auto=format&fit=crop" },
            { name: "Elena Volkov", role: "Yoga & Mobility", img: "https://images.unsplash.com/photo-1548690312-e3b507d17a4d?q=80&w=1974&auto=format&fit=crop" }
          ].map((trainer, i) => (
            <div key={i} className="group relative overflow-hidden rounded-3xl aspect-[4/5]">
              <img src={trainer.img} className="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110" alt={trainer.name} />
              <div className="absolute inset-0 bg-gradient-to-t from-zinc-950 via-transparent to-transparent opacity-90" />
              <div className="absolute bottom-0 left-0 p-8 w-full translate-y-4 group-hover:translate-y-0 transition-transform">
                <h4 className="text-2xl font-black italic">{trainer.name}</h4>
                <p className="text-lime-400 font-bold uppercase text-sm tracking-widest">{trainer.role}</p>
              </div>
            </div>
          ))}
        </div>
      </section>
    </>
  );

  const Programs = () => (
    <section className="py-24 bg-zinc-950 pt-32 min-h-screen">
      <div className="max-w-7xl mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-5xl font-black italic mb-4">CHOOSE YOUR DISCIPLINE</h2>
          <p className="text-gray-400 max-w-xl mx-auto">Diverse training programs designed to challenge every muscle and mindset.</p>
        </div>

        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          {[
            { title: "Power Lifting", level: "Advanced", time: "60-90 min", icon: <Dumbbell />, color: "bg-red-500" },
            { title: "Metabolic HIIT", level: "All Levels", time: "45 min", icon: <Flame />, color: "bg-orange-500" },
            { title: "Flexibility & Flow", level: "Beginner", time: "60 min", icon: <HeartPulse />, color: "bg-blue-500" },
            { title: "Tactical Boxing", level: "Intermediate", time: "60 min", icon: <Trophy />, color: "bg-yellow-500" },
            { title: "Body Sculpting", level: "All Levels", time: "50 min", icon: <Users />, color: "bg-purple-500" },
            { title: "Core Blast", level: "All Levels", time: "30 min", icon: <Flame />, color: "bg-lime-500" }
          ].map((prog, i) => (
            <div key={i} className="bg-zinc-900 rounded-3xl p-1 overflow-hidden group border border-zinc-800 hover:border-lime-400 transition-all">
              <div className="p-8">
                <div className={`${prog.color} w-12 h-12 rounded-xl flex items-center justify-center mb-6 text-white group-hover:scale-110 transition-transform`}>
                  {prog.icon}
                </div>
                <h3 className="text-2xl font-black italic mb-2 uppercase">{prog.title}</h3>
                <div className="flex gap-4 mb-6">
                  <span className="text-xs font-bold px-3 py-1 bg-zinc-800 rounded-full text-gray-300">{prog.level}</span>
                  <span className="text-xs font-bold px-3 py-1 bg-zinc-800 rounded-full text-gray-300">{prog.time}</span>
                </div>
                <p className="text-gray-400 mb-8">Comprehensive training that pushes your cardiovascular and muscular endurance to new heights.</p>
                <button className="w-full py-4 rounded-xl border border-zinc-700 font-bold hover:bg-white hover:text-zinc-900 transition-all">
                  Book Class
                </button>
              </div>
            </div>
          ))}
        </div>
      </div>
    </section>
  );

  const Blog = () => (
    <section className="py-24 bg-zinc-950 pt-32 min-h-screen">
      <div className="max-w-7xl mx-auto px-4">
        <div className="flex flex-col md:flex-row md:items-end justify-between mb-16 gap-6">
          <div>
            <h2 className="text-5xl font-black italic mb-4 uppercase">Pulse Feed</h2>
            <p className="text-gray-400">Expert advice on nutrition, recovery, and fitness philosophy.</p>
          </div>
          <div className="flex gap-2">
            <button className="px-6 py-2 bg-lime-400 text-zinc-900 rounded-full font-bold">All</button>
            <button className="px-6 py-2 bg-zinc-900 text-gray-400 rounded-full font-bold hover:text-white">Nutrition</button>
            <button className="px-6 py-2 bg-zinc-900 text-gray-400 rounded-full font-bold hover:text-white">Training</button>
          </div>
        </div>

        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-10">
          {[
            { 
              cat: "Nutrition", 
              title: "The Ultimate Guide to Macro Tracking", 
              date: "Oct 12, 2023", 
              img: "https://images.unsplash.com/photo-1490645935967-10de6ba17061?q=80&w=2053&auto=format&fit=crop",
              excerpt: "Learn how to calculate and balance your proteins, carbs, and fats for maximum growth."
            },
            { 
              cat: "Training", 
              title: "5 Exercises for Exploding Core Power", 
              date: "Oct 09, 2023", 
              img: "https://images.unsplash.com/photo-1517836357463-d25dfeac3438?q=80&w=2070&auto=format&fit=crop",
              excerpt: "Beyond crunches: how to build functional strength that protects your spine."
            },
            { 
              cat: "Recovery", 
              title: "The Science of Sleep and Muscle Repair", 
              date: "Oct 05, 2023", 
              img: "https://images.unsplash.com/photo-1541781774459-bb2af2f05b55?q=80&w=2060&auto=format&fit=crop",
              excerpt: "Why your 8 hours of rest might be the most important part of your training plan."
            },
            { 
              cat: "Dietary Tips", 
              title: "Hydration: More Than Just Drinking Water", 
              date: "Sep 28, 2023", 
              img: "https://images.unsplash.com/photo-1523362628745-0c100150b504?q=80&w=1935&auto=format&fit=crop",
              excerpt: "Electrolytes, timing, and how to tell if you're actually performing at peak hydration."
            },
            { 
              cat: "Lifestyle", 
              title: "Mental Grit: Winning the Inner War", 
              date: "Sep 20, 2023", 
              img: "https://images.unsplash.com/photo-1526506118085-60ce8714f8c5?q=80&w=1974&auto=format&fit=crop",
              excerpt: "Strategies to stay motivated when the initial excitement of a new routine fades."
            },
            { 
              cat: "Nutrition", 
              title: "Plant-Based Gains: High Protein Vegan Diets", 
              date: "Sep 15, 2023", 
              img: "https://images.unsplash.com/photo-1512621776951-a57141f2eefd?q=80&w=2070&auto=format&fit=crop",
              excerpt: "How to hit your 200g protein goal without touching a single animal product."
            }
          ].map((post, i) => (
            <div key={i} className="group cursor-pointer">
              <div className="overflow-hidden rounded-3xl mb-6 relative aspect-video">
                <img src={post.img} className="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" alt={post.title} />
                <div className="absolute top-4 left-4 bg-lime-400 text-zinc-900 px-4 py-1 rounded-full text-xs font-black uppercase">
                  {post.cat}
                </div>
              </div>
              <div className="text-gray-500 text-sm font-bold uppercase tracking-widest mb-2">{post.date}</div>
              <h3 className="text-2xl font-black italic mb-3 group-hover:text-lime-400 transition-colors uppercase leading-tight">
                {post.title}
              </h3>
              <p className="text-gray-400 line-clamp-2 leading-relaxed">{post.excerpt}</p>
            </div>
          ))}
        </div>
      </div>
    </section>
  );

  const Pricing = () => (
    <section className="py-24 bg-zinc-950 pt-32 min-h-screen">
      <div className="max-w-7xl mx-auto px-4">
        <div className="text-center mb-16">
          <h2 className="text-5xl font-black italic mb-4">MEMBERSHIP PLANS</h2>
          <p className="text-gray-400 max-w-xl mx-auto">Flexible options for every commitment level. No hidden fees, just pure value.</p>
        </div>

        <div className="grid md:grid-cols-3 gap-8 items-center">
          {[
            { 
              name: "Basic Pulse", 
              price: "29", 
              features: ["Gym floor access", "Locker room access", "Basic workout plan", "1 Free guest pass/mo"],
              highlight: false 
            },
            { 
              name: "Iron Elite", 
              price: "59", 
              features: ["24/7 Access", "All classes included", "Advanced nutrition guide", "Sauna & Steam room", "Monthly PT session"],
              highlight: true 
            },
            { 
              name: "Power Pro", 
              price: "99", 
              features: ["Unlimited PT", "Custom supplement plan", "Massage therapy", "VIP Lounge access", "Free apparel quarterly"],
              highlight: false 
            }
          ].map((plan, i) => (
            <div key={i} className={`rounded-[2rem] p-8 ${plan.highlight ? 'bg-lime-400 text-zinc-900 py-16 shadow-2xl scale-105 z-10' : 'bg-zinc-900 text-white border border-zinc-800'}`}>
              {plan.highlight && (
                <div className="bg-zinc-900 text-lime-400 text-[10px] font-black uppercase tracking-widest py-1 px-4 rounded-full inline-block mb-6">Most Popular</div>
              )}
              <h3 className="text-2xl font-black italic mb-2 uppercase">{plan.name}</h3>
              <div className="flex items-baseline gap-1 mb-8">
                <span className="text-4xl font-black">$</span>
                <span className="text-6xl font-black italic tracking-tighter">{plan.price}</span>
                <span className={`text-sm font-bold uppercase ${plan.highlight ? 'text-zinc-700' : 'text-gray-500'}`}>/month</span>
              </div>
              
              <ul className="space-y-4 mb-10">
                {plan.features.map((feat, idx) => (
                  <li key={idx} className="flex items-center gap-3 font-bold text-sm">
                    <CheckCircle2 size={18} className={plan.highlight ? 'text-zinc-900' : 'text-lime-400'} />
                    {feat}
                  </li>
                ))}
              </ul>

              <button className={`w-full py-4 rounded-2xl font-black text-lg transition-all ${plan.highlight ? 'bg-zinc-900 text-white hover:bg-zinc-800' : 'bg-lime-400 text-zinc-900 hover:bg-lime-500'}`}>
                Choose Plan
              </button>
            </div>
          ))}
        </div>
      </div>
    </section>
  );

  const Contact = () => (
    <section className="py-24 bg-zinc-950 pt-32 min-h-screen">
      <div className="max-w-7xl mx-auto px-4">
        <div className="grid lg:grid-cols-2 gap-20">
          <div>
            <h2 className="text-5xl font-black italic mb-6 uppercase">Get In Touch</h2>
            <p className="text-gray-400 mb-12 text-lg">Have questions about our programs or want to book a tour of the facility? Reach out to us anytime.</p>
            
            <div className="space-y-8">
              <div className="flex items-start gap-6">
                <div className="bg-zinc-900 p-4 rounded-2xl text-lime-400">
                  <MapPin size={24} />
                </div>
                <div>
                  <h4 className="font-bold text-lg mb-1">Our Location</h4>
                  <p className="text-gray-400">123 Fitness Ave, Iron District<br />New York, NY 10001</p>
                </div>
              </div>
              <div className="flex items-start gap-6">
                <div className="bg-zinc-900 p-4 rounded-2xl text-lime-400">
                  <Phone size={24} />
                </div>
                <div>
                  <h4 className="font-bold text-lg mb-1">Call Us</h4>
                  <p className="text-gray-400">+1 (555) 987-6543</p>
                </div>
              </div>
              <div className="flex items-start gap-6">
                <div className="bg-zinc-900 p-4 rounded-2xl text-lime-400">
                  <Mail size={24} />
                </div>
                <div>
                  <h4 className="font-bold text-lg mb-1">Email</h4>
                  <p className="text-gray-400">support@ironpulse.fit</p>
                </div>
              </div>
            </div>
          </div>

          <div className="bg-zinc-900 p-10 rounded-[3rem] border border-zinc-800">
            <h3 className="text-2xl font-black italic mb-8 uppercase">Send a Message</h3>
            <form className="space-y-6" onSubmit={(e) => e.preventDefault()}>
              <div className="grid md:grid-cols-2 gap-6">
                <div>
                  <label className="block text-xs font-bold uppercase text-gray-500 mb-2">Full Name</label>
                  <input type="text" className="w-full bg-zinc-950 border border-zinc-800 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-lime-400" placeholder="John Doe" />
                </div>
                <div>
                  <label className="block text-xs font-bold uppercase text-gray-500 mb-2">Email Address</label>
                  <input type="email" className="w-full bg-zinc-950 border border-zinc-800 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-lime-400" placeholder="john@example.com" />
                </div>
              </div>
              <div>
                <label className="block text-xs font-bold uppercase text-gray-500 mb-2">Subject</label>
                <select className="w-full bg-zinc-950 border border-zinc-800 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-lime-400">
                  <option>Membership Inquiry</option>
                  <option>Personal Training</option>
                  <option>Class Booking</option>
                  <option>Other</option>
                </select>
              </div>
              <div>
                <label className="block text-xs font-bold uppercase text-gray-500 mb-2">Message</label>
                <textarea rows="4" className="w-full bg-zinc-950 border border-zinc-800 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-lime-400" placeholder="Your message here..."></textarea>
              </div>
              <button className="w-full py-4 bg-lime-400 text-zinc-900 rounded-xl font-black uppercase text-lg hover:bg-lime-500 transition-all">
                Send Message
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>
  );

  const Footer = () => (
    <footer className="bg-zinc-950 text-white pt-24 pb-12 border-t border-zinc-900">
      <div className="max-w-7xl mx-auto px-4">
        <div className="grid md:grid-cols-4 gap-12 mb-16">
          <div className="col-span-1 md:col-span-2">
            <div className="flex items-center gap-2 mb-6" onClick={() => navigate('home')}>
              <div className="bg-lime-400 p-1.5 rounded-lg">
                <Dumbbell className="text-zinc-900 w-6 h-6" />
              </div>
              <span className="text-3xl font-black italic tracking-tighter">IRONPULSE</span>
            </div>
            <p className="text-gray-400 max-w-sm mb-8 leading-relaxed">
              Transforming lives through elite training, science-based nutrition, and an unbreakable community. Join the pulse today.
            </p>
            <div className="flex gap-4">
              {[1, 2, 3, 4].map((i) => (
                <div key={i} className="w-10 h-10 bg-zinc-900 rounded-full flex items-center justify-center hover:bg-lime-400 hover:text-zinc-900 transition-all cursor-pointer">
                  <div className="w-5 h-5 bg-current mask-social opacity-80" />
                  <Star size={18} />
                </div>
              ))}
            </div>
          </div>
          
          <div>
            <h4 className="font-black italic uppercase mb-8">Navigation</h4>
            <ul className="space-y-4 text-gray-400 font-bold uppercase text-sm">
              <li className="hover:text-lime-400 cursor-pointer transition-colors" onClick={() => navigate('home')}>Home</li>
              <li className="hover:text-lime-400 cursor-pointer transition-colors" onClick={() => navigate('programs')}>Programs</li>
              <li className="hover:text-lime-400 cursor-pointer transition-colors" onClick={() => navigate('blog')}>Pulse Feed</li>
              <li className="hover:text-lime-400 cursor-pointer transition-colors" onClick={() => navigate('pricing')}>Membership</li>
            </ul>
          </div>

          <div>
            <h4 className="font-black italic uppercase mb-8">Gym Hours</h4>
            <ul className="space-y-4 text-gray-400 font-bold uppercase text-sm">
              <li className="flex justify-between"><span>Mon - Fri</span> <span className="text-white">05:00 - 00:00</span></li>
              <li className="flex justify-between"><span>Saturday</span> <span className="text-white">07:00 - 22:00</span></li>
              <li className="flex justify-between"><span>Sunday</span> <span className="text-white">08:00 - 20:00</span></li>
              <li className="text-lime-400 mt-4 italic">* Elite Members: 24/7 Access</li>
            </ul>
          </div>
        </div>
        
        <div className="pt-12 border-t border-zinc-900 text-center text-gray-500 text-sm font-bold uppercase tracking-widest">
          &copy; {new Date().getFullYear()} IronPulse Fitness. All Rights Reserved.
        </div>
      </div>
    </footer>
  );

  return (
    <div className="min-h-screen bg-zinc-950 font-sans selection:bg-lime-400 selection:text-zinc-900">
      <Navbar />
      
      <main className="animate-in fade-in duration-700">
        {activeTab === 'home' && <HomeContent />}
        {activeTab === 'programs' && <Programs />}
        {activeTab === 'blog' && <Blog />}
        {activeTab === 'pricing' && <Pricing />}
        {activeTab === 'contact' && <Contact />}
      </main>

      <Footer />
      
      {/* Floating CTA for Mobile */}
      <div className="fixed bottom-6 right-6 md:hidden z-40">
        <button 
          onClick={() => navigate('contact')}
          className="w-14 h-14 bg-lime-400 rounded-full shadow-2xl flex items-center justify-center text-zinc-900"
        >
          <Mail size={24} />
        </button>
      </div>
    </div>
  );
};

export default App;
