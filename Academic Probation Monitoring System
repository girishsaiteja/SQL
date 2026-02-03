-- Tables
CREATE TABLE students (
  student_id NUMERIC PRIMARY KEY,
  name VARCHAR2(100)
);

CREATE TABLE marks (
  student_id NUMBER PRIMARY KEY,
  subject1 NUMBER,
  subject2 NUMBER,
  subject3 NUMBER,
  subject4 NUMBER,
  subject5 NUMBER,
  subject6 NUMBER
);

CREATE TABLE gpa_info (
  student_id NUMBER PRIMARY KEY,
  cgpa NUMBER(4,2),
  flagged CHAR(1)
);

-- Function to compute CGPA
CREATE OR REPLACE FUNCTION calculate_cgpa (
  s1 NUMBER, s2 NUMBER, s3 NUMBER,
  s4 NUMBER, s5 NUMBER, s6 NUMBER
) RETURN NUMBER IS
BEGIN
  RETURN ROUND((s1 + s2 + s3 + s4 + s5 + s6)/6/10, 2);
END;
/

-- Trigger to populate gpa_info
CREATE OR REPLACE TRIGGER trg_insert_gpa
AFTER INSERT ON marks
FOR EACH ROW
BEGIN
  DECLARE
    cg NUMBER(4,2);
    flg CHAR(1);
  BEGIN
    cg := calculate_cgpa(
      :NEW.subject1, :NEW.subject2, :NEW.subject3,
      :NEW.subject4, :NEW.subject5, :NEW.subject6
    );
    flg := CASE WHEN cg < 4 THEN 'Y' ELSE 'N' END;
    INSERT INTO gpa_info VALUES (:NEW.student_id, cg, flg);
  END;
END;
/

-- Insert student names
INSERT INTO students VALUES (1, 'Alice');
INSERT INTO students VALUES (2, 'Bob');
INSERT INTO students VALUES (3, 'Catherine');
INSERT INTO students VALUES (4, 'David');
INSERT INTO students VALUES (5, 'Eva');
INSERT INTO students VALUES (6, 'Frank');
INSERT INTO students VALUES (7, 'Grace');
INSERT INTO students VALUES (8, 'Henry');
INSERT INTO students VALUES (9, 'Isha');
INSERT INTO students VALUES (10, 'Jack');
INSERT INTO students VALUES (11, 'Kavya');
INSERT INTO students VALUES (12, 'Liam');
INSERT INTO students VALUES (13, 'Maya');
INSERT INTO students VALUES (14, 'Nikhil');
INSERT INTO students VALUES (15, 'Olivia');
INSERT INTO students VALUES (16, 'Pranav');
INSERT INTO students VALUES (17, 'Qiana');
INSERT INTO students VALUES (18, 'Ravi');
INSERT INTO students VALUES (19, 'Sophie');
INSERT INTO students VALUES (20, 'Taran');

-- Insert marks 
BEGIN
  INSERT INTO marks VALUES (1, 78, 82, 75, 80, 70, 85);  
  INSERT INTO marks VALUES (2, 45, 50, 48, 55, 46, 49);  
  INSERT INTO marks VALUES (3, 88, 92, 90, 91, 87, 89);  
  INSERT INTO marks VALUES (4, 60, 62, 59, 58, 61, 60);  
  INSERT INTO marks VALUES (5, 30, 35, 40, 38, 25, 33);  
  INSERT INTO marks VALUES (6, 90, 91, 93, 92, 95, 94);  
  INSERT INTO marks VALUES (7, 50, 55, 52, 54, 53, 51);  
  INSERT INTO marks VALUES (8, 95, 97, 94, 96, 92, 91);  
  INSERT INTO marks VALUES (9, 48, 45, 46, 44, 42, 43);  
  INSERT INTO marks VALUES (10, 70, 72, 75, 71, 68, 74); 
  INSERT INTO marks VALUES (11, 35, 38, 36, 39, 34, 37); 
  INSERT INTO marks VALUES (12, 85, 82, 83, 84, 80, 81); 
  INSERT INTO marks VALUES (13, 76, 78, 79, 80, 75, 77); 
  INSERT INTO marks VALUES (14, 66, 68, 65, 67, 69, 70); 
  INSERT INTO marks VALUES (15, 59, 58, 57, 60, 62, 61); 
  INSERT INTO marks VALUES (16, 44, 42, 43, 41, 45, 40); 
  INSERT INTO marks VALUES (17, 91, 93, 90, 89, 94, 95); 
  INSERT INTO marks VALUES (18, 73, 72, 75, 74, 70, 71); 
  INSERT INTO marks VALUES (19, 55, 54, 53, 52, 56, 57); 
  INSERT INTO marks VALUES (20, 68, 69, 67, 66, 70, 71); 
END;
/


SET SERVEROUTPUT ON;
DECLARE
  CURSOR cur_flagged IS
    SELECT s.student_id, s.name, g.cgpa
    FROM students s
    JOIN gpa_info g ON s.student_id = g.student_id
    WHERE g.flagged = 'Y';
  v_id   students.student_id%TYPE;
  v_name students.name%TYPE;
  v_cgpa gpa_info.cgpa%TYPE;
BEGIN
  FOR student_rec IN cur_flagged LOOP
    v_id := student_rec.student_id;
    v_name := student_rec.name;
    v_cgpa := student_rec.cgpa;

    DBMS_OUTPUT.PUT_LINE('Student ID: ' || v_id);
    DBMS_OUTPUT.PUT_LINE('Name      : ' || v_name);
    DBMS_OUTPUT.PUT_LINE('CGPA      : ' || TO_CHAR(v_cgpa, '0.00'));
    DBMS_OUTPUT.PUT_LINE('Flagged   : Yes');
    DBMS_OUTPUT.PUT_LINE('-----------------------------');
  END LOOP;
END;
/
