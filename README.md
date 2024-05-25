# React Modal - Form Fields

```js
npm install react-bootstrap bootstrap react-icons --save
npm install gh-pages --save-dev
"homepage": "https://dev-arindam-roy.github.io/react-modal-form-fields-application",
"scripts": {
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build",
}
```

```js
import React, { useState } from "react";
import {
  FaPlus,
  FaRegTrashAlt,
  FaRegTimesCircle,
  FaRegSave,
} from "react-icons/fa";
import Container from "react-bootstrap/Container";
import Row from "react-bootstrap/Row";
import Col from "react-bootstrap/Col";
import Card from "react-bootstrap/Card";
import Button from "react-bootstrap/Button";
import Modal from "react-bootstrap/Modal";
import Form from "react-bootstrap/Form";
import Table from 'react-bootstrap/Table';

const App = () => {
  const [modal, setModal] = useState(false);
  const [user, setUser] = useState({ name: "", email: "", mobile: "" });
  const [userList, setUserList] = useState([]);
  const [isFormValidate, setIsFormValidate] = useState(false);
  const modalHandleClose = () => {
    formReset();
    setModal(false);
  };
  const modalHandleShow = () => {
    setModal(true);
  };
  const addUserFormSubmitHandler = () => {
    if (user.name !== "" && user.email !== "" && user.mobile !== "") {
      setUserList([...userList, user]);
      formReset();
      setModal(false);
    }
  };
  const checkFieldValidation = () => {
    if (user.name === "" || user.email === "" || user.mobile === "") {
      setIsFormValidate(false);
    } else {
      setIsFormValidate(true);
    }
  }
  const formReset = () => {
    setUser({ name: "", email: "", mobile: "" });
    setIsFormValidate(false);
  }
  const deleteUserListHandler = () => {
    setUserList([]);
    formReset();
  }
  return (
    <>
      <Container fluid="md">
        <Row className="mt-3">
          <Col md={{ span: 8, offset: 2 }}>
            <Card>
              <Card.Header>
                <Row>
                  <Col md={9}>
                    <h3>Users: ({userList.length})</h3>
                  </Col>
                  <Col md={3} style={{ textAlign: "right" }}>
                    <Button variant="primary" onClick={modalHandleShow}>
                      <FaPlus /> Add User
                    </Button>
                  </Col>
                </Row>
              </Card.Header>
              <Card.Body>
                <Table striped bordered hover size="sm">
                  <thead>
                    <tr>
                      <th>SL</th>
                      <th>NAME</th>
                      <th>EMAIL ID</th>
                      <th>MOBILE NO</th>
                    </tr>
                  </thead>
                  <tbody>
                    {
                      userList.length > 0 && (
                        userList.map((item, index) => {
                          return (
                            <tr key={"userTr" + index}>
                              <th>{index + 1}</th>
                              <td>{item.name}</td>
                              <td>{item.email}</td>
                              <td>{item.mobile}</td>
                            </tr>
                          )
                        })
                      )
                    }
                    {
                      userList.length === 0 && (
                        <tr>
                          <td colSpan={4}>No users found!</td>
                        </tr>
                      )
                    }
                  </tbody>
                </Table>
              </Card.Body>
              <Card.Footer style={{ textAlign: "right" }}>
                {
                  userList.length > 0 && (
                    <Button variant="danger" onClick={deleteUserListHandler}>
                      <FaRegTrashAlt /> Delete All
                    </Button>
                  )
                }
              </Card.Footer>
            </Card>
          </Col>
        </Row>
      </Container>

      <Modal
        show={modal}
        backdrop="static"
        keyboard={false}
        size="mb"
        aria-labelledby="contained-user-modal-title-vcenter"
        centered
        onHide={modalHandleClose}
      >
        <Modal.Header closeButton>
          <Modal.Title id="contained-user-modal-title-vcenter">
            <label>
              <FaPlus /> Add New User
            </label>
          </Modal.Title>
        </Modal.Header>
        <Modal.Body>
          <Row>
            <Col md={12} xs={12}>
              <Form id="addUserModalForm">
                <Form.Group className="mb-3" controlId="forName">
                  <Form.Label>
                    Name: <em>*</em>
                  </Form.Label>
                  <Form.Control
                    type="text"
                    name="name"
                    placeholder="Enter Name"
                    required
                    value={user.name}
                    onChange={(e) => setUser({...user, name: e.target.value})}
                    onBlur={checkFieldValidation}
                  />
                </Form.Group>
                <Form.Group className="mb-3" controlId="forName">
                  <Form.Label>
                    Email: <em>*</em>
                  </Form.Label>
                  <Form.Control
                    type="email"
                    name="email"
                    placeholder="Enter Email Id"
                    required
                    value={user.email}
                    onChange={(e) => setUser({...user, email: e.target.value})}
                    onBlur={checkFieldValidation}
                  />
                </Form.Group>
                <Form.Group className="mb-3" controlId="forName">
                  <Form.Label>
                    Mobile: <em>*</em>
                  </Form.Label>
                  <Form.Control
                    type="tel"
                    name="mobile"
                    placeholder="Enter Mobile No"
                    required
                    value={user.mobile}
                    onChange={(e) => setUser({...user, mobile: e.target.value})}
                    onBlur={checkFieldValidation}
                  />
                </Form.Group>
              </Form>
            </Col>
          </Row>
        </Modal.Body>
        <Modal.Footer>
          <Button variant="danger" onClick={modalHandleClose}>
            <FaRegTimesCircle /> Close
          </Button>
          <Button variant="primary" onClick={addUserFormSubmitHandler} className={((!isFormValidate) ? ' disabled' : ' ')}>
            <FaRegSave /> Save
          </Button>
        </Modal.Footer>
      </Modal>
    </>
  );
};

export default App;

```