# Celebel-project-3import React from "react";
import { BrowserRouter as Router, Routes, Route, Link } from "react-router-dom";
import { useState } from "react";
import { LineChart, Line, XAxis, YAxis, Tooltip, CartesianGrid, ResponsiveContainer } from "recharts";

const data = [
  { name: 'Jan', uv: 400 },
  { name: 'Feb', uv: 300 },
  { name: 'Mar', uv: 200 },
  { name: 'Apr', uv: 278 },
  { name: 'May', uv: 189 }
];

const TableComponent = () => (
  <div className="p-4">
    <h2 className="text-xl font-bold mb-4">User Table</h2>
    <table className="min-w-full border">
      <thead>
        <tr className="bg-gray-200">
          <th className="py-2 px-4 border">ID</th>
          <th className="py-2 px-4 border">Name</th>
          <th className="py-2 px-4 border">Email</th>
        </tr>
      </thead>
      <tbody>
        {[1, 2, 3].map(id => (
          <tr key={id}>
            <td className="py-2 px-4 border">{id}</td>
            <td className="py-2 px-4 border">User {id}</td>
            <td className="py-2 px-4 border">user{id}@example.com</td>
          </tr>
        ))}
      </tbody>
    </table>
  </div>
);

const ChartComponent = () => (
  <div className="p-4">
    <h2 className="text-xl font-bold mb-4">Sales Chart</h2>
    <ResponsiveContainer width="100%" height={300}>
      <LineChart data={data}>
        <CartesianGrid stroke="#ccc" />
        <XAxis dataKey="name" />
        <YAxis />
        <Tooltip />
        <Line type="monotone" dataKey="uv" stroke="#8884d8" />
      </LineChart>
    </ResponsiveContainer>
  </div>
);

const CalendarComponent = () => (
  <div className="p-4">
    <h2 className="text-xl font-bold mb-4">Calendar</h2>
    <p>Integrate with a library like `react-calendar` here.</p>
  </div>
);

const KanbanBoard = () => (
  <div className="p-4">
    <h2 className="text-xl font-bold mb-4">Kanban Board</h2>
    <div className="grid grid-cols-3 gap-4">
      {['To Do', 'In Progress', 'Done'].map(stage => (
        <div key={stage} className="bg-gray-100 p-4 rounded">
          <h3 className="font-semibold mb-2">{stage}</h3>
          <div className="bg-white p-2 rounded shadow">Task for {stage}</div>
        </div>
      ))}
    </div>
  </div>
);

const ThemeSwitcher = ({ theme, toggleTheme }) => (
  <button onClick={toggleTheme} className="absolute top-4 right-4 px-4 py-2 bg-indigo-600 text-white rounded">
    Toggle {theme === 'light' ? 'Dark' : 'Light'} Theme
  </button>
);

const Layout = ({ children, theme, toggleTheme }) => (
  <div className={`${theme === 'dark' ? 'bg-gray-900 text-white' : 'bg-white text-black'} min-h-screen`}>
    <nav className="p-4 border-b">
      <ul className="flex gap-4">
        <li><Link to="/">Home</Link></li>
        <li><Link to="/table">Table</Link></li>
        <li><Link to="/chart">Chart</Link></li>
        <li><Link to="/calendar">Calendar</Link></li>
        <li><Link to="/kanban">Kanban</Link></li>
      </ul>
    </nav>
    <ThemeSwitcher theme={theme} toggleTheme={toggleTheme} />
    <main>{children}</main>
  </div>
);

const DashboardApp = () => {
  const [theme, setTheme] = useState("light");
  const toggleTheme = () => setTheme(prev => (prev === "light" ? "dark" : "light"));

  return (
    <Router>
      <Layout theme={theme} toggleTheme={toggleTheme}>
        <Routes>
          <Route path="/" element={<h2 className="p-4 text-xl">Welcome to the Admin Dashboard</h2>} />
          <Route path="/table" element={<TableComponent />} />
          <Route path="/chart" element={<ChartComponent />} />
          <Route path="/calendar" element={<CalendarComponent />} />
          <Route path="/kanban" element={<KanbanBoard />} />
        </Routes>
      </Layout>
    </Router>
  );
};

export default DashboardApp;
