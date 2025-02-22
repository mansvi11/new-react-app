# new-react-app
import React, { createContext, useState, useContext } from "react";
import { BrowserRouter as Router, Routes, Route, Link } from "react-router-dom";
import styled, { ThemeProvider } from "styled-components";

const Theme = {
  primaryColor: "#007bff",
  backgroundColor: "#f8f9fa",
};

const GlobalContext = createContext();
const useGlobal = () => useContext(GlobalContext);

const AppProvider = ({ children }) => {
  const [count, setCount] = useState(0);
  return (
    <GlobalContext.Provider value={{ count, setCount }}>
      {children}
    </GlobalContext.Provider>
  );
};

const Home = () => {
  const { count, setCount } = useGlobal();
  return (
    <Container>
      <h1>Welcome to the Improved React App</h1>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
      <StyledLink to="/about">Go to About</StyledLink>
    </Container>
  );
};

const About = () => (
  <Container>
    <h1>About Page</h1>
    <StyledLink to="/">Back to Home</StyledLink>
  </Container>
);

const App = () => {
  return (
    <ThemeProvider theme={Theme}>
      <AppProvider>
        <Router>
          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
          </Routes>
        </Router>
      </AppProvider>
    </ThemeProvider>
  );
};

const Container = styled.div`
  text-align: center;
  padding: 20px;
  background-color: ${(props) => props.theme.backgroundColor};
  color: ${(props) => props.theme.primaryColor};
`;

const StyledLink = styled(Link)`
  display: block;
  margin-top: 20px;
  color: ${(props) => props.theme.primaryColor};
  text-decoration: none;
  font-weight: bold;
`;

export default App;
