import { Toaster } from 'react-hot-toast';
import { useAppStore } from './store/appStore';
import LandingPage from './components/LandingPage';
import AuthPage from './components/AuthPage';
import OnboardingPage from './components/OnboardingPage';
import Sidebar from './components/Sidebar';
import Dashboard from './components/Dashboard';
import JobScanner from './components/JobScanner';
import RealTimeScanner from './components/RealTimeScanner';
import ResumeEngine from './components/ResumeEngine';
import CompanyAnalysis from './components/CompanyAnalysis';
import CoverLetterGenerator from './components/CoverLetterGenerator';
import EmailComposer from './components/EmailComposer';
import AutoApply from './components/AutoApply';
import Applications from './components/Applications';
import Analytics from './components/Analytics';
import InterviewAI from './components/InterviewAI';
import AIChat from './components/AIChat';
import SettingsPage from './components/SettingsPage';
import GoogleJobSearch from './components/GoogleJobSearch';
import NotificationSettings from './components/NotificationSettings';
import { WhatsAppToast, NotificationBell } from './components/WhatsAppPopup';
import DeployPage from './components/DeployPage';
import { Menu, User } from 'lucide-react';

function AppContent() {
  const { currentPage, isLoggedIn, sidebarOpen, setSidebarOpen, user, setCurrentPage } = useAppStore();

  // Landing page for non-logged in users
  if (!isLoggedIn && currentPage === 'landing') {
    return <LandingPage />;
  }

  // Auth page
  if (!isLoggedIn || currentPage === 'auth') {
    return <AuthPage />;
  }

  // Onboarding for new users
  if (currentPage === 'onboarding') {
    return <OnboardingPage />;
  }

  const renderPage = () => {
    switch (currentPage) {
      case 'dashboard': return <Dashboard />;
      case 'scanner': return <RealTimeScanner />;
      case 'googlesearch': return <GoogleJobSearch />;
      case 'jobs': return <JobScanner />;
      case 'notifications': return <NotificationSettings />;
      case 'resume': return <ResumeEngine />;
      case 'company': return <CompanyAnalysis />;
      case 'coverletter': return <CoverLetterGenerator />;
      case 'email': return <EmailComposer />;
      case 'autoapply': return <AutoApply />;
      case 'applications': return <Applications />;
      case 'analytics': return <Analytics />;
      case 'interview': return <InterviewAI />;
      case 'chat': return <AIChat />;
      case 'deploy': return <DeployPage />;
      case 'settings': return <SettingsPage />;
      default: return <Dashboard />;
    }
  };

  return (
    <div className="min-h-screen bg-dark-900">
      <Sidebar />
      
      {/* Main Content */}
      <div
        className="transition-all duration-300 max-lg:!ml-0"
        style={{ marginLeft: sidebarOpen ? 256 : 72 }}
      >
        {/* Top Bar */}
        <header className="sticky top-0 z-30 h-14 bg-dark-900/80 backdrop-blur-xl border-b border-white/5 flex items-center justify-between px-4 sm:px-6">
          <button
            onClick={() => setSidebarOpen(true)}
            className="lg:hidden p-2 rounded-lg hover:bg-dark-700 text-gray-400"
          >
            <Menu className="w-5 h-5" />
          </button>
          
          <div className="flex items-center gap-3 ml-auto">
            <div className="flex items-center gap-2 px-3 py-1.5 bg-dark-800 border border-white/5 rounded-full">
              <div className="w-2 h-2 rounded-full bg-cyber-green animate-pulse" />
              <span className="text-xs text-gray-400">AI Active</span>
            </div>
            
            {/* Notification Bell */}
            <NotificationBell />
            
            {/* User Profile */}
            <button
              onClick={() => setCurrentPage('settings')}
              className="flex items-center gap-2 px-3 py-1.5 bg-dark-800 border border-white/5 rounded-full hover:border-primary-500/30 transition-all"
            >
              <div className="w-6 h-6 rounded-full bg-gradient-to-br from-primary-500 to-purple-500 flex items-center justify-center">
                <User className="w-3 h-3 text-white" />
              </div>
              <span className="text-xs text-gray-300 hidden sm:block">{user.name || 'Profile'}</span>
            </button>
          </div>
        </header>

        {/* Page Content */}
        <main className="p-4 sm:p-6">
          {renderPage()}
        </main>
      </div>
    </div>
  );
}

export default function App() {
  return (
    <>
      <Toaster
        position="top-right"
        toastOptions={{
          style: {
            background: '#1a1a2e',
            color: '#e2e8f0',
            border: '1px solid rgba(255,255,255,0.05)',
          },
        }}
      />
      <AppContent />
      <WhatsAppToast />
    </>
  );
}
