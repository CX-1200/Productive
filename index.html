import React, { useState, useEffect, useMemo, useRef } from 'react';
import { initializeApp } from 'firebase/app';
import { 
  getAuth, 
  signInAnonymously, 
  signInWithCustomToken,
  onAuthStateChanged,
} from 'firebase/auth';
import { 
  getFirestore, 
  collection, 
  doc, 
  addDoc, 
  updateDoc, 
  deleteDoc, 
  onSnapshot, 
  query, 
  orderBy, 
  where,
  serverTimestamp
} from 'firebase/firestore';
import { 
  Calendar, 
  CheckSquare, 
  CreditCard, 
  Layout, 
  ChevronLeft, 
  ChevronRight, 
  Plus, 
  Trash2, 
  MoreVertical, 
  Search, 
  Filter, 
  User, 
  ArrowRight,
  RefreshCw,
  DollarSign,
  TrendingUp,
  TrendingDown,
  Link as LinkIcon,
  Archive,
  Clock,
  Briefcase
} from 'lucide-react';

// --- Firebase Initialization ---
const firebaseConfig = JSON.parse(__firebase_config || '{}');
const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);
const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';

// --- Utility Functions ---

// Get ISO Week Number
const getWeekNumber = (d) => {
  d = new Date(Date.UTC(d.getFullYear(), d.getMonth(), d.getDate()));
  d.setUTCDate(d.getUTCDate() + 4 - (d.getUTCDay() || 7));
  const yearStart = new Date(Date.UTC(d.getUTCFullYear(), 0, 1));
  const weekNo = Math.ceil((((d - yearStart) / 86400000) + 1) / 7);
  return { week: weekNo, year: d.getUTCFullYear() };
};

// Get dates for a specific week number
const getDateRangeOfWeek = (w, y) => {
  const d = new Date(Date.UTC(y, 0, 1 + (w - 1) * 7));
  const day = d.getUTCDay();
  const diff = d.getUTCDate() - day + (day === 0 ? -6 : 1);
  const monday = new Date(d.setDate(diff));
  
  const dates = [];
  for (let i = 0; i < 7; i++) {
    const nextDate = new Date(monday);
    nextDate.setDate(monday.getDate() + i);
    dates.push(nextDate.toISOString().split('T')[0]);
  }
  return dates;
};

// Get Day Index (0 = Sunday, 1 = Monday, ..., 6 = Saturday)
const getDayIndex = (dateStr) => {
    const date = new Date(dateStr);
    // Adjust to Monday=0, Sunday=6 for column mapping
    const day = date.getDay();
    return day === 0 ? 6 : day - 1; 
};

// Format Currency
const formatCurrency = (amount) => {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
  }).format(amount);
};

// --- Main App Component ---

export default function App() {
  const [user, setUser] = useState(null);
  const [mode, setMode] = useState('kanban'); // 'kanban' | 'budget'
  const [loading, setLoading] = useState(true);

  // Auth Flow
  useEffect(() => {
    const initAuth = async () => {
      try {
        if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
          await signInWithCustomToken(auth, __initial_auth_token);
        } else {
          await signInAnonymously(auth);
        }
      } catch (err) {
        console.error("Auth failed", err);
      }
    };
    initAuth();
    const unsubscribe = onAuthStateChanged(auth, (u) => {
      setUser(u);
      setLoading(false);
    });
    return () => unsubscribe();
  }, []);

  if (loading) return <div className="flex h-screen items-center justify-center bg-gray-50 text-gray-500">Loading App...</div>;
  if (!user) return <div className="flex h-screen items-center justify-center bg-gray-50 text-red-500">Authentication Error. Please refresh.</div>;

  return (
    <div className="min-h-screen bg-gray-100 font-sans text-slate-800">
      <Header mode={mode} setMode={setMode} user={user} />
      <main className="p-2 md:p-4 h-[calc(100vh-64px)] overflow-hidden">
        {mode === 'kanban' ? (
          <KanbanBoard user={user} />
        ) : (
          <BudgetManager user={user} setMode={setMode} />
        )}
      </main>
    </div>
  );
}

// --- Header ---
function Header({ mode, setMode, user }) {
  const [title, setTitle] = useState("My Workspace");
  const [isEditing, setIsEditing] = useState(false);

  // Persist title to local storage for simplicity in this demo, 
  // or could be firestore 'settings' doc
  useEffect(() => {
    const saved = localStorage.getItem(`app_title_${user.uid}`);
    if (saved) setTitle(saved);
  }, [user]);

  const saveTitle = () => {
    setIsEditing(false);
    localStorage.setItem(`app_title_${user.uid}`, title);
  };

  return (
    <header className="h-16 bg-white border-b border-gray-200 flex items-center justify-between px-4 shadow-sm z-20 relative">
      <div className="flex items-center gap-4">
        <div 
          onClick={() => setMode(mode === 'kanban' ? 'budget' : 'kanban')}
          className="cursor-pointer flex items-center gap-2 px-3 py-1.5 rounded-lg hover:bg-gray-100 transition-colors"
          title="Click to Switch Application Mode"
        >
          <div className={`p-2 rounded-md ${mode === 'kanban' ? 'bg-blue-100 text-blue-600' : 'bg-emerald-100 text-emerald-600'}`}>
            {mode === 'kanban' ? <Layout size={20} /> : <CreditCard size={20} />}
          </div>
          <div className="flex flex-col">
             <span className="text-xs font-semibold text-gray-400 uppercase tracking-wider">Current Mode</span>
             <span className="font-bold text-sm md:text-base leading-tight">
               {mode === 'kanban' ? 'Kanban Manager' : 'Budget Tracker'}
             </span>
          </div>
        </div>

        <div className="h-8 w-px bg-gray-200 mx-2 hidden md:block"></div>

        {isEditing ? (
          <input 
            type="text" 
            value={title} 
            onChange={(e) => setTitle(e.target.value)}
            onBlur={saveTitle}
            onKeyDown={(e) => e.key === 'Enter' && saveTitle()}
            autoFocus
            className="text-lg font-bold text-gray-800 border-b-2 border-blue-500 focus:outline-none bg-transparent"
          />
        ) : (
          <h1 
            onClick={() => setIsEditing(true)}
            className="text-lg md:text-xl font-bold text-gray-800 cursor-text hover:text-blue-600 truncate max-w-[200px] md:max-w-md"
          >
            {title}
          </h1>
        )}
      </div>
      
      <div className="flex items-center gap-2">
        <div className="hidden md:flex items-center gap-2 px-3 py-1 bg-gray-50 rounded-full border border-gray-200">
           <User size={14} className="text-gray-400"/>
           <span className="text-xs text-gray-500 font-mono">{user.uid.slice(0, 6)}</span>
        </div>
      </div>
    </header>
  );
}

// --- Kanban Implementation ---
function KanbanBoard({ user }) {
  const [currentDate, setCurrentDate] = useState(new Date());
  const [tasks, setTasks] = useState([]);
  const [viewMode, setViewMode] = useState('weekdays'); // 'weekdays' | 'weekend'
  const [filterStatus, setFilterStatus] = useState('All');
  const [searchTerm, setSearchTerm] = useState('');
  const [showUnassigned, setShowUnassigned] = useState(true);
  const [showHistory, setShowHistory] = useState(false);
  const [draggedTask, setDraggedTask] = useState(null);

  // Calculations for Week
  const { week, year } = getWeekNumber(currentDate);
  const weekDates = useMemo(() => getDateRangeOfWeek(week, year), [week, year]);
  const currentWeekStart = weekDates[0];

  // Data Fetching
  useEffect(() => {
    if (!user) return;
    const q = collection(db, 'artifacts', appId, 'users', user.uid, 'tasks');
    const unsubscribe = onSnapshot(q, (snapshot) => {
      const data = snapshot.docs.map(d => ({ id: d.id, ...d.data() }));
      setTasks(data);
    });
    return () => unsubscribe();
  }, [user]);

  // Derived State: Organize tasks
  const organizedTasks = useMemo(() => {
    const result = {
      unassigned: [],
      days: weekDates.reduce((acc, date) => ({ ...acc, [date]: [] }), {}), // Initialize 7 days
    };
    
    tasks.forEach(task => {
      // 1. Filter out Completed/Cancelled tasks from the main board
      if (task.status === 'Completed' || task.status === 'Cancelled') return;

      // 2. Search Filter
      if (searchTerm && !task.title.toLowerCase().includes(searchTerm.toLowerCase())) return;
      // 3. Status Filter
      if (filterStatus !== 'All' && task.status !== filterStatus) return;

      if (!task.assignedDate) {
        // Task has no assigned date (Backlog)
        result.unassigned.push(task);
      } else {
        const taskDate = task.assignedDate;
        
        // A. Task is assigned to this week
        if (weekDates.includes(taskDate)) {
          result.days[taskDate].push(task);
        } 
        // B. Rollover Logic: Past, unfinished tasks
        else if (taskDate < currentWeekStart) {
          // Determine the day of the week the task was originally assigned to (0=Mon, 6=Sun)
          const originalDayIndex = getDayIndex(taskDate);
          
          // Map this index to the corresponding date in the *currently viewed* week (weekDates)
          // For example, a task assigned to last Monday (index 0) is rolled over to this Monday (weekDates[0])
          const targetDate = weekDates[originalDayIndex];
          
          // Push to the target day, marking it as a rollover task
          if (result.days[targetDate]) {
             result.days[targetDate].push({ ...task, isRollover: true, originalDate: taskDate });
          }
        }
        // C. Future tasks are naturally hidden because they don't match weekDates
      }
    });

    return result;
  }, [tasks, weekDates, searchTerm, filterStatus, currentWeekStart]);

  // Handlers
  const handleDragStart = (e, task) => {
    setDraggedTask(task);
    e.dataTransfer.setData('text/plain', task.id);
    e.dataTransfer.effectAllowed = 'move';
  };

  const handleDrop = async (e, targetDate) => {
    e.preventDefault();
    const taskId = e.dataTransfer.getData('text/plain');
    if (!taskId) return;

    try {
      const taskRef = doc(db, 'artifacts', appId, 'users', user.uid, 'tasks', taskId);
      await updateDoc(taskRef, {
        assignedDate: targetDate // null for unassigned, date string for days
      });
    } catch (err) {
      console.error("Drop failed", err);
    }
    setDraggedTask(null);
  };

  const jumpWeek = (delta) => {
    const newDate = new Date(currentDate);
    newDate.setDate(newDate.getDate() + (delta * 7));
    setCurrentDate(newDate);
  };
  
  // Columns to display based on viewMode
  const columnsToShow = useMemo(() => {
    const allColumns = [0, 1, 2, 3, 4, 5, 6]; // Mon-Sun
    if (viewMode === 'weekdays') {
      return allColumns.slice(0, 5); // Mon-Fri (Indices 0-4)
    } else if (viewMode === 'weekend') {
      return allColumns.slice(5); // Sat-Sun (Indices 5-6)
    }
    return allColumns;
  }, [viewMode]);

  return (
    <div className="flex flex-col h-full gap-4">
      
      {showHistory && <TaskHistoryModal user={user} onClose={() => setShowHistory(false)} />}
      
      {/* Kanban Toolbar */}
      <div className="flex flex-col md:flex-row gap-4 justify-between bg-white p-3 rounded-xl shadow-sm border border-gray-200 shrink-0">
        <div className="flex items-center gap-3">
          <div className="flex items-center bg-gray-100 rounded-lg p-1">
            <button onClick={() => jumpWeek(-1)} className="p-1 hover:bg-white rounded shadow-sm transition"><ChevronLeft size={18}/></button>
            <span className="px-3 font-medium text-sm w-32 text-center">Week {week}, {year}</span>
            <button onClick={() => jumpWeek(1)} className="p-1 hover:bg-white rounded shadow-sm transition"><ChevronRight size={18}/></button>
          </div>
          <button 
            onClick={() => setCurrentDate(new Date())}
            className="text-xs font-semibold text-blue-600 hover:underline"
          >
            Today
          </button>
        </div>

        <div className="flex flex-wrap items-center gap-2">
          {/* History Button */}
          <button 
            onClick={() => setShowHistory(true)}
            className="flex items-center gap-1 bg-gray-50 hover:bg-gray-100 text-gray-600 px-3 py-1.5 rounded-lg text-sm font-medium shadow-sm border border-gray-200 transition-all"
          >
            <Archive size={16} /> History
          </button>
          
          {/* View Mode Toggle */}
          <div className="flex items-center bg-gray-100 rounded-lg p-1 text-sm font-medium">
             <button 
               onClick={() => setViewMode('weekdays')}
               className={`px-3 py-1.5 rounded-lg transition-colors ${viewMode === 'weekdays' ? 'bg-white shadow text-blue-700' : 'text-gray-600 hover:bg-gray-200'}`}
             >
               Weekdays
             </button>
             <button 
               onClick={() => setViewMode('weekend')}
               className={`px-3 py-1.5 rounded-lg transition-colors ${viewMode === 'weekend' ? 'bg-white shadow text-blue-700' : 'text-gray-600 hover:bg-gray-200'}`}
             >
               Weekend
             </button>
          </div>


          <div className="relative group">
            <Search className="absolute left-2.5 top-2 text-gray-400" size={14} />
            <input 
              type="text" 
              placeholder="Search..." 
              value={searchTerm}
              onChange={(e) => setSearchTerm(e.target.value)}
              className="pl-8 pr-3 py-1.5 bg-gray-50 border border-gray-200 rounded-lg text-sm focus:ring-2 focus:ring-blue-500 focus:outline-none w-32 md:w-48"
            />
          </div>
          
          <select 
            value={filterStatus} 
            onChange={(e) => setFilterStatus(e.target.value)}
            className="px-2 py-1.5 bg-gray-50 border border-gray-200 rounded-lg text-sm"
          >
            <option value="All">All Status</option>
            <option value="Not Started">Not Started</option>
            <option value="In Progress">In Progress</option>
            <option value="On Hold">On Hold</option>
          </select>

          <button 
            onClick={() => setShowUnassigned(!showUnassigned)}
            className={`md:hidden px-3 py-1.5 text-xs font-medium rounded-lg border ${showUnassigned ? 'bg-indigo-50 border-indigo-200 text-indigo-700' : 'bg-white'}`}
          >
            Backlog
          </button>

          <TaskModal user={user} mode="create" trigger={
             <button className="flex items-center gap-1 bg-blue-600 hover:bg-blue-700 text-white px-3 py-1.5 rounded-lg text-sm font-medium shadow-sm transition-all">
               <Plus size={16} /> New Task
             </button>
          }/>
        </div>
      </div>

      {/* Board Area */}
      <div className="flex-1 overflow-hidden flex gap-4">
        
        {/* Unassigned / Backlog Sidebar */}
        <div className={`${showUnassigned ? 'flex' : 'hidden'} md:flex flex-col w-full md:w-64 bg-slate-50 border border-slate-200 rounded-xl overflow-hidden shrink-0 transition-all`}>
          <div 
             className="p-3 bg-slate-100 border-b border-slate-200 flex justify-between items-center cursor-pointer"
             onDragOver={(e) => e.preventDefault()}
             onDrop={(e) => handleDrop(e, null)}
          >
            <span className="font-semibold text-slate-700 text-sm flex items-center gap-2">
              <Clock size={16} className="text-slate-500"/>
              Unassigned Backlog
            </span>
            <span className="bg-slate-200 text-slate-600 px-1.5 rounded text-xs">{organizedTasks.unassigned.length}</span>
          </div>
          <div 
            className="flex-1 overflow-y-auto p-2 space-y-2"
          >
            {organizedTasks.unassigned.map(task => (
              <TaskCard key={task.id} task={task} user={user} onDragStart={handleDragStart} />
            ))}
            {organizedTasks.unassigned.length === 0 && (
              <div className="text-center py-8 text-slate-400 text-xs italic">Drop tasks here to unassign</div>
            )}
          </div>
        </div>

        {/* Days Columns */}
        <div className="flex-1 overflow-x-auto overflow-y-hidden">
          <div className="flex h-full gap-3 min-w-max pb-2">
            {columnsToShow.map(index => {
              const dateStr = weekDates[index];
              const dateObj = new Date(dateStr);
              const dayName = dateObj.toLocaleDateString('en-US', { weekday: 'short' });
              
              // Date format change: (dd/mm)
              const dayNum = dateObj.getDate().toString().padStart(2, '0');
              const monthNum = (dateObj.getMonth() + 1).toString().padStart(2, '0');
              const dateLabel = `${dayNum}/${monthNum}`;

              const isToday = new Date().toISOString().split('T')[0] === dateStr;
              const isWeekend = index >= 5;

              return (
                <div 
                  key={dateStr} 
                  className={`flex flex-col w-72 md:w-64 rounded-xl border overflow-hidden shrink-0 transition-colors ${
                    isToday ? 'bg-blue-50/50 border-blue-200' : 'bg-white border-gray-200'
                  } ${isWeekend ? 'bg-amber-50/50' : ''}`}
                  onDragOver={(e) => { e.preventDefault(); e.currentTarget.classList.add('bg-blue-50'); }}
                  onDragLeave={(e) => { e.currentTarget.classList.remove('bg-blue-50'); }}
                  onDrop={(e) => { e.currentTarget.classList.remove('bg-blue-50'); handleDrop(e, dateStr); }}
                >
                  <div className={`p-3 border-b flex justify-between items-baseline ${isToday ? 'border-blue-100' : 'border-gray-100'}`}>
                     <div>
                       <span className={`text-sm font-bold ${isToday ? 'text-blue-700' : 'text-gray-700'}`}>{dayName}</span>
                       <span className={`ml-1 text-xs ${isToday ? 'text-blue-500' : 'text-gray-500'}`}>({dateLabel})</span>
                     </div>
                     <TaskModal user={user} mode="create" prefillDate={dateStr} trigger={
                       <button className="text-gray-400 hover:text-blue-600"><Plus size={16}/></button>
                     } />
                  </div>

                  <div className="flex-1 overflow-y-auto p-2 space-y-2">
                    {organizedTasks.days[dateStr].map(task => (
                      <TaskCard key={task.id} task={task} user={user} onDragStart={handleDragStart} />
                    ))}
                    {organizedTasks.days[dateStr].length === 0 && (
                      <div className="h-full min-h-[50px] flex items-center justify-center">
                         <div className="w-full h-full border-2 border-dashed border-gray-100 rounded-lg"></div>
                      </div>
                    )}
                  </div>
                </div>
              );
            })}
          </div>
        </div>

      </div>
    </div>
  );
}

// --- Task Card ---
function TaskCard({ task, user, onDragStart }) {
  const statusColors = {
    'Not Started': 'bg-gray-100 text-gray-600',
    'In Progress': 'bg-amber-100 text-amber-700',
    'Completed': 'bg-emerald-100 text-emerald-700',
    'Cancelled': 'bg-red-50 text-red-400 decoration-line-through',
    'On Hold': 'bg-purple-100 text-purple-700'
  };
  
  const statusMenuOptions = ['Not Started', 'In Progress', 'On Hold', 'Completed', 'Cancelled'];
  const [showStatusMenu, setShowStatusMenu] = useState(false);
  const menuRef = useRef(null);

  // Close menu when clicking outside
  useEffect(() => {
    const handleClickOutside = (event) => {
      if (menuRef.current && !menuRef.current.contains(event.target)) {
        setShowStatusMenu(false);
      }
    };
    document.addEventListener("mousedown", handleClickOutside);
    return () => document.removeEventListener("mousedown", handleClickOutside);
  }, []);

  const updateStatus = async (newStatus) => {
    setShowStatusMenu(false);
    await updateDoc(doc(db, 'artifacts', appId, 'users', user.uid, 'tasks', task.id), {
      status: newStatus,
      // Ensure completionDate is set correctly (only if status is completed or cancelled)
      completionDate: (newStatus === 'Completed' || newStatus === 'Cancelled') ? new Date().toISOString().split('T')[0] : null
    });
  };

  const rolloverDate = task.isRollover 
    ? new Date(task.originalDate).toLocaleDateString('en-US', { day: '2-digit', month: '2-digit' })
    : null;

  return (
    <div 
      draggable 
      onDragStart={(e) => onDragStart(e, task)}
      className={`bg-white p-3 rounded-lg border shadow-sm cursor-grab active:cursor-grabbing hover:shadow-md transition-all group relative border-l-4 ${
        task.isRollover ? 'border-l-red-400' : 'border-l-transparent'
      }`}
    >
      {task.isRollover && (
        <div className="absolute top-1 right-2 text-[10px] font-bold text-red-500 uppercase tracking-wide flex items-center gap-1">
          <RefreshCw size={10} /> OVERDUE (From {rolloverDate})
        </div>
      )}
      
      <div className="flex justify-between items-start mb-2">
        <div className="relative" ref={menuRef}>
          <button 
            onClick={() => setShowStatusMenu(!showStatusMenu)}
            className={`text-xs px-2 py-0.5 rounded-full font-medium transition-colors ${statusColors[task.status] || 'bg-gray-100'}`}
          >
            {task.status}
          </button>

          {showStatusMenu && (
            <div className="absolute left-0 mt-1 w-36 bg-white border border-gray-200 rounded-lg shadow-lg z-10">
              {statusMenuOptions.map(status => (
                <button
                  key={status}
                  onClick={() => updateStatus(status)}
                  className={`block w-full text-left px-3 py-1 text-sm ${
                    task.status === status ? 'bg-blue-50 text-blue-600 font-semibold' : 'hover:bg-gray-50 text-gray-700'
                  }`}
                >
                  {status}
                </button>
              ))}
            </div>
          )}
        </div>

        <div className="opacity-0 group-hover:opacity-100 transition-opacity">
           <TaskModal user={user} mode="edit" task={task} trigger={
             <button className="text-gray-400 hover:text-blue-500"><MoreVertical size={14} /></button>
           }/>
        </div>
      </div>
      
      <h4 className={`text-sm font-semibold text-gray-800 mb-1 line-clamp-2 ${task.status === 'Cancelled' ? 'line-through text-gray-400' : ''}`}>
        {task.title}
      </h4>
      
      {task.type && (
        <span className="text-[10px] text-gray-500 uppercase tracking-wider border border-gray-100 px-1 rounded bg-gray-50 flex items-center w-fit">
          <Briefcase size={10} className="mr-1"/>{task.type}
        </span>
      )}

      {task.notes && <p className="text-xs text-gray-500 mt-2 line-clamp-2">{task.notes}</p>}

      {/* Quick Actions Footer */}
      <div className="mt-3 pt-2 border-t border-gray-50 flex justify-between items-center">
        <div className="flex -space-x-1">
          {task.assignees && task.assignees.map((a, i) => (
             <div key={i} className="w-5 h-5 rounded-full bg-blue-100 border border-white flex items-center justify-center text-[8px] text-blue-800 font-bold" title={a}>
               {a.charAt(0)}
             </div>
          ))}
        </div>
        <div className="flex gap-1">
          {task.status !== 'Completed' && (
            <button 
              onClick={() => updateStatus('Completed')}
              className="p-1 hover:bg-emerald-50 text-gray-300 hover:text-emerald-600 rounded" 
              title="Mark Complete"
            >
              <CheckSquare size={14} />
            </button>
          )}
        </div>
      </div>
    </div>
  );
}

// --- Task History Modal ---
function TaskHistoryModal({ user, onClose }) {
    const [historyTasks, setHistoryTasks] = useState([]);
    const [loading, setLoading] = useState(true);

    useEffect(() => {
        if (!user) return;
        setLoading(true);
        
        // Removed orderBy to fix the index error.
        // We filter for 'Completed' or 'Cancelled' tasks.
        const q = query(
            collection(db, 'artifacts', appId, 'users', user.uid, 'tasks'),
            where('status', 'in', ['Completed', 'Cancelled']),
        );
        
        const unsubscribe = onSnapshot(q, (snapshot) => {
            let data = snapshot.docs.map(d => ({ id: d.id, ...d.data() }));
            
            // Sort in JavaScript by completionDate descending (most recent first)
            data.sort((a, b) => {
                const dateA = a.completionDate || '0';
                const dateB = b.completionDate || '0';
                
                // Compare dates lexicographically (assuming YYYY-MM-DD format)
                if (dateA < dateB) return 1;
                if (dateA > dateB) return -1;
                return 0;
            });
            
            setHistoryTasks(data);
            setLoading(false);
        }, (error) => {
            console.error("Error fetching history:", error);
            setLoading(false);
        });
        return () => unsubscribe();
    }, [user]);


    return (
        <div className="fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4">
          <div className="bg-white rounded-xl shadow-2xl w-full max-w-2xl h-5/6 flex flex-col overflow-hidden animate-in fade-in zoom-in duration-200">
            <div className="p-4 border-b flex justify-between items-center bg-gray-50">
              <h3 className="font-bold text-gray-800 flex items-center gap-2"><Archive size={20}/> Task History (Completed / Cancelled)</h3>
              <button onClick={onClose} className="text-gray-400 hover:text-gray-600 text-xl">&times;</button>
            </div>
            
            <div className="flex-1 overflow-y-auto p-4 space-y-3">
              {loading ? (
                  <div className="text-center py-12 text-gray-500">Loading history...</div>
              ) : historyTasks.length === 0 ? (
                  <div className="text-center py-12 text-gray-400">No completed or cancelled tasks found yet.</div>
              ) : (
                  historyTasks.map(task => (
                      <div key={task.id} className={`p-3 rounded-lg border shadow-sm ${task.status === 'Completed' ? 'bg-emerald-50 border-emerald-200' : 'bg-red-50 border-red-200'}`}>
                          <div className="flex justify-between items-center">
                              <h4 className={`font-semibold ${task.status === 'Cancelled' ? 'line-through text-gray-500' : 'text-gray-800'}`}>
                                  {task.title}
                              </h4>
                              <span className={`text-xs px-2 py-0.5 rounded-full font-medium ${task.status === 'Completed' ? 'bg-emerald-200 text-emerald-800' : 'bg-red-200 text-red-800'}`}>
                                  {task.status}
                              </span>
                          </div>
                          <p className="text-xs text-gray-600 mt-1">{task.notes}</p>
                          <div className="text-[10px] text-gray-400 mt-2 border-t pt-1 border-gray-100 flex justify-between">
                            <span>Type: {task.type}</span>
                            <span>
                                {task.completionDate ? `Date: ${new Date(task.completionDate).toLocaleDateString()}` : 'Date info unavailable'}
                            </span>
                          </div>
                      </div>
                  ))
              )}
            </div>
            
            <div className="p-4 border-t bg-gray-50 text-right">
                <button onClick={onClose} className="px-4 py-2 text-sm bg-gray-200 text-gray-700 rounded-lg hover:bg-gray-300 font-medium">Close</button>
            </div>
          </div>
        </div>
    );
}

// --- Budget Manager (Unchanged) ---
function BudgetManager({ user, setMode }) {
  const [transactions, setTransactions] = useState([]);
  const [tasks, setTasks] = useState([]); // For linking
  const [summary, setSummary] = useState({ income: 0, expense: 0, balance: 0 });
  const [categoryFilter, setCategoryFilter] = useState('All');

  // Fetch Transactions
  useEffect(() => {
    if (!user) return;
    const q = query(
      collection(db, 'artifacts', appId, 'users', user.uid, 'transactions'),
      orderBy('date', 'desc')
    );
    const unsubscribe = onSnapshot(q, (snapshot) => {
      const data = snapshot.docs.map(d => ({ id: d.id, ...d.data() }));
      setTransactions(data);
      
      // Calculate Summary
      const sum = data.reduce((acc, curr) => {
        const amt = parseFloat(curr.amount);
        if (curr.type === 'income') acc.income += amt;
        else acc.expense += amt;
        return acc;
      }, { income: 0, expense: 0 });
      setSummary({ ...sum, balance: sum.income - sum.expense });
    });
    return () => unsubscribe();
  }, [user]);

  // Fetch Tasks for Linking context
  useEffect(() => {
    if (!user) return;
    const q = collection(db, 'artifacts', appId, 'users', user.uid, 'tasks');
    const unsubscribe = onSnapshot(q, (snapshot) => {
      setTasks(snapshot.docs.map(d => ({ id: d.id, ...d.data() })));
    });
    return () => unsubscribe();
  }, [user]);

  const filteredTransactions = transactions.filter(t => 
    categoryFilter === 'All' ? true : t.category === categoryFilter
  );

  return (
    <div className="h-full flex flex-col md:flex-row gap-6 max-w-6xl mx-auto">
      {/* Left: Summary & Charts */}
      <div className="w-full md:w-1/3 flex flex-col gap-4">
        <div className="bg-gradient-to-br from-slate-800 to-slate-900 text-white p-6 rounded-2xl shadow-lg">
          <h2 className="text-slate-400 text-sm font-medium uppercase tracking-wider mb-1">Total Balance</h2>
          <div className="text-4xl font-bold mb-6">{formatCurrency(summary.balance)}</div>
          
          <div className="grid grid-cols-2 gap-4">
             <div className="bg-white/10 p-3 rounded-xl backdrop-blur-sm">
                <div className="flex items-center gap-2 text-emerald-300 text-xs mb-1">
                  <TrendingUp size={14} /> Income
                </div>
                <div className="font-semibold text-lg">{formatCurrency(summary.income)}</div>
             </div>
             <div className="bg-white/10 p-3 rounded-xl backdrop-blur-sm">
                <div className="flex items-center gap-2 text-rose-300 text-xs mb-1">
                  <TrendingDown size={14} /> Expenses
                </div>
                <div className="font-semibold text-lg">{formatCurrency(summary.expense)}</div>
             </div>
          </div>
        </div>

        {/* Categories Quick View */}
        <div className="bg-white p-4 rounded-xl border border-gray-200 shadow-sm flex-1">
          <h3 className="font-bold text-gray-700 mb-4">Categories</h3>
          <div className="space-y-3">
             {['Food', 'Transport', 'Housing', 'Entertainment', 'Utilities', 'Salary', 'Freelance'].map(cat => {
                const total = transactions
                  .filter(t => t.category === cat)
                  .reduce((sum, t) => sum + parseFloat(t.amount), 0);
                if (total === 0) return null;
                return (
                  <div key={cat} className="flex justify-between items-center text-sm">
                    <span className="text-gray-600">{cat}</span>
                    <span className="font-mono font-medium">{formatCurrency(total)}</span>
                  </div>
                )
             })}
          </div>
        </div>
      </div>

      {/* Right: Transactions List */}
      <div className="flex-1 bg-white rounded-xl border border-gray-200 shadow-sm flex flex-col overflow-hidden">
        <div className="p-4 border-b border-gray-100 flex justify-between items-center bg-gray-50/50">
          <h3 className="font-bold text-gray-800">Transactions</h3>
          <TransactionModal user={user} tasks={tasks} trigger={
            <button className="flex items-center gap-2 bg-slate-900 text-white px-4 py-2 rounded-lg text-sm hover:bg-slate-800 transition">
              <Plus size={16} /> Add Entry
            </button>
          }/>
        </div>

        <div className="p-2 border-b border-gray-100">
           <div className="flex gap-2 overflow-x-auto pb-2">
             {['All', 'Food', 'Transport', 'Utilities', 'Salary'].map(cat => (
               <button 
                key={cat}
                onClick={() => setCategoryFilter(cat)}
                className={`px-3 py-1 rounded-full text-xs font-medium whitespace-nowrap transition-colors ${categoryFilter === cat ? 'bg-slate-800 text-white' : 'bg-gray-100 text-gray-600 hover:bg-gray-200'}`}
               >
                 {cat}
               </button>
             ))}
           </div>
        </div>

        <div className="flex-1 overflow-y-auto">
          {filteredTransactions.length === 0 ? (
            <div className="flex flex-col items-center justify-center h-48 text-gray-400">
              <DollarSign size={32} className="mb-2 opacity-50"/>
              <p>No transactions found</p>
            </div>
          ) : (
            <table className="w-full text-left border-collapse">
              <thead className="bg-gray-50 sticky top-0 text-xs uppercase text-gray-500 font-semibold">
                <tr>
                  <th className="p-3 pl-4">Category</th>
                  <th className="p-3">Details</th>
                  <th className="p-3 text-right">Amount</th>
                  <th className="p-3 w-10"></th>
                </tr>
              </thead>
              <tbody className="divide-y divide-gray-100">
                {filteredTransactions.map(t => {
                   const linkedTask = tasks.find(task => task.id === t.linkedTaskId);
                   return (
                    <tr key={t.id} className="hover:bg-gray-50 group transition-colors">
                      <td className="p-3 pl-4">
                        <span className={`inline-block px-2 py-0.5 rounded text-xs font-medium ${t.type === 'income' ? 'bg-emerald-100 text-emerald-700' : 'bg-rose-100 text-rose-700'}`}>
                          {t.category}
                        </span>
                      </td>
                      <td className="p-3">
                        <div className="text-sm font-medium text-gray-800">{t.note || 'No description'}</div>
                        <div className="text-xs text-gray-400 flex items-center gap-2 mt-0.5">
                           {new Date(t.date).toLocaleDateString()}
                           {linkedTask && (
                             <span 
                               className="flex items-center gap-1 text-blue-500 bg-blue-50 px-1.5 rounded cursor-pointer hover:underline"
                               onClick={() => setMode('kanban')}
                             >
                               <LinkIcon size={10} /> Linked: {linkedTask.title.slice(0, 15)}...
                             </span>
                           )}
                        </div>
                      </td>
                      <td className={`p-3 text-right font-mono text-sm font-semibold ${t.type === 'income' ? 'text-emerald-600' : 'text-slate-700'}`}>
                        {t.type === 'expense' && '-'}{formatCurrency(t.amount)}
                      </td>
                      <td className="p-3 text-right">
                         <button 
                            onClick={() => deleteDoc(doc(db, 'artifacts', appId, 'users', user.uid, 'transactions', t.id))}
                            className="text-gray-300 hover:text-red-500 opacity-0 group-hover:opacity-100 transition-all"
                         >
                           <Trash2 size={16} />
                         </button>
                      </td>
                    </tr>
                   )
                })}
              </tbody>
            </table>
          )}
        </div>
      </div>
    </div>
  );
}

// --- Modals (Task & Transaction - Unchanged logic, TaskModal has new 'Payment' type) ---

function TaskModal({ user, mode = 'create', task = null, trigger, prefillDate = null }) {
  const [isOpen, setIsOpen] = useState(false);
  const [formData, setFormData] = useState({
    title: '',
    type: 'Task',
    status: 'Not Started',
    notes: '',
    assignedDate: prefillDate || '',
    assigneeStr: ''
  });

  useEffect(() => {
    if (isOpen && mode === 'edit' && task) {
      setFormData({
        title: task.title,
        type: task.type || 'Task',
        status: task.status,
        notes: task.notes || '',
        assignedDate: task.assignedDate || '',
        assigneeStr: task.assignees ? task.assignees.join(', ') : ''
      });
    } else if (isOpen && mode === 'create') {
        // Reset or set prefill
        setFormData(prev => ({ 
            ...prev, 
            assignedDate: prefillDate || '',
            title: '', type: 'Task', status: 'Not Started', notes: '', assigneeStr: ''
        }));
    }
  }, [isOpen, task, mode, prefillDate]);

  const handleSubmit = async (e) => {
    e.preventDefault();
    const payload = {
      title: formData.title,
      type: formData.type,
      status: formData.status,
      notes: formData.notes,
      assignedDate: formData.assignedDate || null,
      assignees: formData.assigneeStr.split(',').map(s => s.trim()).filter(s => s),
      updatedAt: serverTimestamp()
    };
    
    // Set completion date if the task is being completed or cancelled
    if (formData.status === 'Completed' || formData.status === 'Cancelled') {
        payload.completionDate = new Date().toISOString().split('T')[0];
    } else {
        payload.completionDate = null;
    }


    try {
      if (mode === 'create') {
        await addDoc(collection(db, 'artifacts', appId, 'users', user.uid, 'tasks'), {
            ...payload,
            createdAt: serverTimestamp()
        });
      } else {
        await updateDoc(doc(db, 'artifacts', appId, 'users', user.uid, 'tasks', task.id), payload);
      }
      setIsOpen(false);
      // Reset form if create
      if (mode === 'create') setFormData({ title: '', type: 'Task', status: 'Not Started', notes: '', assignedDate: '', assigneeStr: '' });
    } catch (error) {
      console.error("Error saving task:", error);
      // Custom modal/message box instead of alert()
      // alert("Failed to save task"); 
    }
  };

  const handleDelete = async () => {
      // Using window.confirm just for a rapid confirmation step in this modal handler.
      // In a production app, this should be replaced with a custom modal UI.
      if(window.confirm('Are you sure you want to delete this task permanently?')) {
          await deleteDoc(doc(db, 'artifacts', appId, 'users', user.uid, 'tasks', task.id));
          setIsOpen(false);
      }
  }

  return (
    <>
      <div onClick={() => setIsOpen(true)}>{trigger}</div>
      
      {isOpen && (
        <div className="fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4">
          <div className="bg-white rounded-xl shadow-xl w-full max-w-md overflow-hidden animate-in fade-in zoom-in duration-200">
            <div className="p-4 border-b flex justify-between items-center bg-gray-50">
              <h3 className="font-bold text-gray-800">{mode === 'create' ? 'New Task' : 'Edit Task'}</h3>
              <button type="button" onClick={() => setIsOpen(false)} className="text-gray-400 hover:text-gray-600 text-xl">&times;</button>
            </div>
            
            <form onSubmit={handleSubmit} className="p-4 space-y-4">
              <div>
                <label className="block text-xs font-semibold text-gray-500 uppercase mb-1">Title</label>
                <input 
                  required
                  type="text" 
                  className="w-full border rounded-lg p-2 text-sm focus:ring-2 focus:ring-blue-500 outline-none"
                  value={formData.title}
                  onChange={e => setFormData({...formData, title: e.target.value})}
                  placeholder="E.g., Finish Q4 Report"
                />
              </div>

              <div className="grid grid-cols-2 gap-4">
                <div>
                   <label className="block text-xs font-semibold text-gray-500 uppercase mb-1">Type (User-Defined)</label>
                   <select 
                     className="w-full border rounded-lg p-2 text-sm bg-white"
                     value={formData.type}
                     onChange={e => setFormData({...formData, type: e.target.value})}
                   >
                     <option>Task</option>
                     <option>Project</option>
                     <option>Bug</option>
                     <option>Meeting</option>
                     <option>Payment</option>
                     <option>Idea</option>
                   </select>
                   <p className="text-[10px] text-gray-400 mt-1">Custom options can be managed here.</p>
                </div>
                <div>
                   <label className="block text-xs font-semibold text-gray-500 uppercase mb-1">Status</label>
                   <select 
                     className="w-full border rounded-lg p-2 text-sm bg-white"
                     value={formData.status}
                     onChange={e => setFormData({...formData, status: e.target.value})}
                   >
                     <option>Not Started</option>
                     <option>In Progress</option>
                     <option>On Hold</option>
                     <option>Completed</option>
                     <option>Cancelled</option>
                   </select>
                </div>
              </div>

              <div>
                <label className="block text-xs font-semibold text-gray-500 uppercase mb-1">Assigned Date</label>
                <input 
                  type="date" 
                  className="w-full border rounded-lg p-2 text-sm text-gray-600"
                  value={formData.assignedDate}
                  onChange={e => setFormData({...formData, assignedDate: e.target.value})}
                />
                <p className="text-[10px] text-gray-400 mt-1">Leave empty to add to Backlog</p>
              </div>

              <div>
                <label className="block text-xs font-semibold text-gray-500 uppercase mb-1">Assignees (Profiles)</label>
                <input 
                  type="text" 
                  className="w-full border rounded-lg p-2 text-sm"
                  value={formData.assigneeStr}
                  onChange={e => setFormData({...formData, assigneeStr: e.target.value})}
                  placeholder="John, Sarah (comma separated profiles)"
                />
              </div>

              <div>
                <label className="block text-xs font-semibold text-gray-500 uppercase mb-1">Notes</label>
                <textarea 
                  className="w-full border rounded-lg p-2 text-sm h-24 resize-none"
                  value={formData.notes}
                  onChange={e => setFormData({...formData, notes: e.target.value})}
                ></textarea>
              </div>

              <div className="flex justify-between items-center pt-2">
                 {mode === 'edit' && (
                     <button type="button" onClick={handleDelete} className="text-red-500 text-sm hover:underline">Delete Task</button>
                 )}
                 <div className="flex gap-2 ml-auto">
                    <button type="button" onClick={() => setIsOpen(false)} className="px-4 py-2 text-sm text-gray-600 hover:bg-gray-100 rounded-lg">Cancel</button>
                    <button type="submit" className="px-4 py-2 text-sm bg-blue-600 text-white rounded-lg hover:bg-blue-700 font-medium">Save Task</button>
                 </div>
              </div>
            </form>
          </div>
        </div>
      )}
    </>
  );
}

function TransactionModal({ user, tasks, trigger }) {
  const [isOpen, setIsOpen] = useState(false);
  const [formData, setFormData] = useState({
    amount: '',
    type: 'expense',
    category: 'Food',
    note: '',
    date: new Date().toISOString().split('T')[0],
    linkedTaskId: ''
  });
  
  const categories = ['Food', 'Transport', 'Housing', 'Utilities', 'Entertainment', 'Salary', 'Freelance', 'Other'];

  const handleSubmit = async (e) => {
    e.preventDefault();
    try {
        await addDoc(collection(db, 'artifacts', appId, 'users', user.uid, 'transactions'), {
            ...formData,
            createdAt: serverTimestamp()
        });
        setIsOpen(false);
        setFormData({ amount: '', type: 'expense', category: 'Food', note: '', date: new Date().toISOString().split('T')[0], linkedTaskId: '' });
    } catch (err) {
        console.error(err);
    }
  }

  return (
    <>
      <div onClick={() => setIsOpen(true)}>{trigger}</div>
      {isOpen && (
        <div className="fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4">
          <div className="bg-white rounded-xl shadow-xl w-full max-w-sm overflow-hidden animate-in fade-in zoom-in duration-200">
             <div className="p-4 border-b bg-gray-50 flex justify-between items-center">
                 <h3 className="font-bold text-gray-800">New Transaction</h3>
                 <button type="button" onClick={() => setIsOpen(false)} className="text-gray-400 text-xl">&times;</button>
             </div>
             <form onSubmit={handleSubmit} className="p-4 space-y-4">
                <div className="flex gap-2 p-1 bg-gray-100 rounded-lg">
                    {['income', 'expense'].map(t => (
                        <button
                          key={t}
                          type="button"
                          onClick={() => setFormData({...formData, type: t})}
                          className={`flex-1 py-1.5 text-sm font-medium rounded-md capitalize transition-all ${formData.type === t ? 'bg-white shadow text-slate-800' : 'text-gray-500'}`}
                        >
                            {t}
                        </button>
                    ))}
                </div>

                <div>
                   <label className="block text-xs font-semibold text-gray-500 uppercase mb-1">Amount</label>
                   <div className="relative">
                       <span className="absolute left-3 top-2 text-gray-400">$</span>
                       <input 
                         required
                         type="number" 
                         step="0.01"
                         className="w-full border rounded-lg pl-6 pr-3 py-2 text-sm font-mono"
                         value={formData.amount}
                         onChange={e => setFormData({...formData, amount: e.target.value})}
                       />
                   </div>
                </div>

                <div>
                    <label className="block text-xs font-semibold text-gray-500 uppercase mb-1">Category</label>
                    <select 
                      className="w-full border rounded-lg p-2 text-sm bg-white"
                      value={formData.category}
                      onChange={e => setFormData({...formData, category: e.target.value})}
                    >
                      {categories.map(c => (
                          <option key={c}>{c}</option>
                      ))}
                    </select>
                </div>

                <div>
                    <label className="block text-xs font-semibold text-gray-500 uppercase mb-1">Date</label>
                    <input 
                      type="date" 
                      className="w-full border rounded-lg p-2 text-sm"
                      value={formData.date}
                      onChange={e => setFormData({...formData, date: e.target.value})}
                    />
                </div>

                <div>
                    <label className="block text-xs font-semibold text-gray-500 uppercase mb-1">Link to Task (Optional)</label>
                    <select 
                       className="w-full border rounded-lg p-2 text-sm bg-white text-gray-700"
                       value={formData.linkedTaskId}
                       onChange={e => setFormData({...formData, linkedTaskId: e.target.value})}
                    >
                        <option value="">-- No Task Linked --</option>
                        {tasks
                         .filter(t => t.status !== 'Completed' && t.status !== 'Cancelled') // Only link active tasks/reminders
                         .map(t => (
                            <option key={t.id} value={t.id}>{t.title}</option>
                        ))}
                    </select>
                    <p className="text-[10px] text-gray-400 mt-1">Useful for tracking project costs or bill payments.</p>
                </div>

                <div>
                    <label className="block text-xs font-semibold text-gray-500 uppercase mb-1">Note</label>
                    <input 
                       type="text"
                       className="w-full border rounded-lg p-2 text-sm"
                       placeholder="Dinner, Uber, etc."
                       value={formData.note}
                       onChange={e => setFormData({...formData, note: e.target.value})}
                    />
                </div>

                <button type="submit" className="w-full py-2 bg-slate-900 text-white rounded-lg font-medium text-sm hover:bg-slate-800">
                    Save Transaction
                </button>
             </form>
          </div>
        </div>
      )}
    </>
  )
}