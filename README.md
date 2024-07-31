# baza_de_date 

1.

Proiectul constă în modelarea unei baze de date pentru un concurs de sah. Aceasta va permite
gestionarea jucătorilor, turneelor, partidelor și clasamentelor. Iată o descriere detaliată a
modelului real, a utilității și a regulilor de funcționare:
1. Jucători:
• Fiecare jucător va fi înregistrat în baza de date cu informații precum nume, vârstă,
țară de origine și clasament ELO.
• Aceste detalii vor fi folosite pentru a identifica și urmări evoluția jucătorilor în
cadrul concursului.
2. Turnee:
• Fiecare turneu va avea un nume, dată și locație în care se va desfășura.
• De asemenea, se pot adăuga informații suplimentare despre reguli specifice și
categorii de participanți.
3. Partide:
• Pentru fiecare turneu, vor exista mai multe partide programate.
• Fiecare partidă va fi înregistrată în baza de date cu detalii precum jucătorii
implicați, data și ora partidei, rezultatul final și mutările efectuate în timpul
partidei.
4. Clasamente:
• Baza de date va include un sistem de calcul al punctajului și actualizare a
clasamentelor pe baza rezultatelor obținute în partidele desfășurate.
• Clasamentele pot fi generate în funcție de turneu, de categoria jucătorilor sau întrun clasament general.
5. Premii:
• În cadrul concursului, se pot oferi premii pentru performanțele obținute de
jucători.
• Baza de date va conține informații despre categoriile de premii, valoarea acestora
și jucătorii câștigători.
6. Înscrieri:
• Jucătorii pot participa la turnee și pot rezerva locuri în avans.
• Baza de date poate include detalii despre rezervările și confirmările de participare
ale jucătorilor.
7. Echipe:
• Jucatorii pot forma echipe pentru a participa la anumite turnee

2.
 
3.
 
4.
-- Crearea tabelului "JUCATORI"
CREATE TABLE JUCATORI (
  id_jucator INT PRIMARY KEY,
  nume VARCHAR(50),
  tara_origine VARCHAR(50),
  rang VARCHAR(50)
);

-- Crearea tabelului "PARTIDE"
CREATE TABLE PARTIDE (
  id_partida INT PRIMARY KEY,
  id_turneu INT,
  id_jucator_1 INT,
  id_jucator_2 INT,
  rezultat_final VARCHAR(50),
  durata INT
);

-- Crearea tabelului "TURNEE"
CREATE TABLE TURNEE (
  id_turneu INT PRIMARY KEY,
  nume VARCHAR(50),
  data_inceput DATE,
  data_sfarsit DATE,
  locatie VARCHAR(50)
);

-- Crearea tabelului "CLASAMENTE"
CREATE TABLE CLASAMENTE (
  id_clasament INT PRIMARY KEY,
  id_turneu INT,
  id_jucator INT,
  punctaj INT,
  pozitie INT
);

-- Crearea tabelului "PREMII"
CREATE TABLE PREMII (
  id_premiu INT PRIMARY KEY,
  valoare INT,
  descriere_premiu VARCHAR(50)
);

-- Crearea tabelului "INSCRIERI"
CREATE TABLE INSCRIERI (
  id_inscriere INT PRIMARY KEY,
  id_turneu INT,
  id_jucator INT,
  stare VARCHAR(50),
  data_inscriere DATE
);

-- Crearea tabelului "ECHIPE"
CREATE TABLE ECHIPE (
  id_echipa INT PRIMARY KEY,
  nume VARCHAR(50),
  id_jucator1 INT,
  id_jucator2 INT
);

-- Crearea tabelului "JUCATORI_TURNEE"
CREATE TABLE JUCATORI_TURNEE (
  id_jucator INT,
  id_turneu INT,
  scor INT,
  PRIMARY KEY (id_jucator, id_turneu)
);

-- Crearea tabelului "JUCATORI_PREMII"
CREATE TABLE JUCATORI_PREMII (
  id_jucator INT,
  id_premiu INT,
  PRIMARY KEY (id_jucator, id_premiu)
);

CREATE TABLE TURNEE_ECHIPE (
  id_turneu_echipa NUMBER,
  id_turneu NUMBER,
  id_echipa NUMBER,
  CONSTRAINT pk_turnee_echipe PRIMARY KEY (id_turneu_echipa),
  CONSTRAINT fk_turnee_echipe_turnee FOREIGN KEY (id_turneu) REFERENCES TURNEE (id_turneu),
  CONSTRAINT fk_turnee_echipe_echipe FOREIGN KEY (id_echipa) REFERENCES ECHIPE (id_echipa)
);

5.

-- Inserarea de date în tabelul "JUCATORI"
INSERT INTO JUCATORI (id_jucator, nume, tara_origine, rang)
SELECT 1, 'John Doe', 'USA', 'Maestru' FROM DUAL UNION ALL
SELECT 2, 'Jane Smith', 'UK', 'Expert' FROM DUAL UNION ALL
SELECT 3, 'Alexandre Leblanc', 'France', 'Maestru' FROM DUAL UNION ALL
SELECT 4, 'Maria Rodriguez', 'Spain', 'Maestru' FROM DUAL UNION ALL
SELECT 5, 'Hans Müller', 'Germany', 'Expert' FROM DUAL UNION ALL
SELECT 6, 'Satoshi Yamamoto', 'Japan', 'Maestru' FROM DUAL UNION ALL
SELECT 7, 'Luca Rossi', 'Italy', 'Expert' FROM DUAL UNION ALL
SELECT 8, 'Ana Popescu', 'Romania', 'Maestru' FROM DUAL UNION ALL
SELECT 9, 'Andrei Petrov', 'Russia', 'Maestru' FROM DUAL UNION ALL
SELECT 10, 'Elena Gomez', 'Spain', 'Expert' FROM DUAL UNION ALL
SELECT 11, 'David Johnson', 'USA', 'Maestru' FROM DUAL UNION ALL
SELECT 12, 'Sophie Martin', 'France', 'Expert' FROM DUAL UNION ALL
SELECT 13, 'Fabio Rossi', 'Italy', 'Maestru' FROM DUAL UNION ALL
SELECT 14, 'Emilia Hernandez', 'Spain', 'Expert' FROM DUAL UNION ALL
SELECT 15, 'Mikhail Ivanov', 'Russia', 'Maestru' FROM DUAL UNION ALL
SELECT 16, 'Lena Schneider', 'Germany', 'Expert' FROM DUAL UNION ALL
SELECT 17, 'Giovanni Bianchi', 'Italy', 'Maestru' FROM DUAL UNION ALL
SELECT 18, 'Simona Popa', 'Romania', 'Expert' FROM DUAL UNION ALL
SELECT 19, 'Ivan Petrov', 'Russia', 'Expert' FROM DUAL UNION ALL
SELECT 20, 'Carmen Fernandez', 'Spain', 'Maestru' FROM DUAL;

  
-- Inserarea de date în tabelul "PARTIDE"
INSERT INTO PARTIDE (id_partida, id_turneu, id_jucator_1, id_jucator_2, rezultat_final, durata)
SELECT 1, 1, 1, 2, 'Victorie', 60 FROM DUAL UNION ALL
SELECT 2, 1, 3, 4, 'Remiza', 45 FROM DUAL UNION ALL
SELECT 3, 2, 5, 6, 'Înfrângere', 30 FROM DUAL UNION ALL
SELECT 4, 2, 7, 8, 'Victorie', 75 FROM DUAL UNION ALL
SELECT 5, 3, 9, 10, 'Remiza', 60 FROM DUAL UNION ALL
SELECT 6, 3, 1, 3, 'Victorie', 90 FROM DUAL UNION ALL
SELECT 7, 4, 2, 4, 'Înfrângere', 45 FROM DUAL UNION ALL
SELECT 8, 4, 5, 7, 'Remiza', 60 FROM DUAL UNION ALL
SELECT 9, 5, 8, 10, 'Victorie', 30 FROM DUAL UNION ALL
SELECT 10, 5, 9, 6, 'Remiza', 45 FROM DUAL UNION ALL
SELECT 11, 1, 11, 12, 'Victorie', 60 FROM DUAL UNION ALL
SELECT 12, 1, 13, 14, 'Remiza', 45 FROM DUAL UNION ALL
SELECT 13, 2, 15, 16, 'Înfrângere', 30 FROM DUAL UNION ALL
SELECT 14, 2, 17, 18, 'Victorie', 75 FROM DUAL UNION ALL
SELECT 15, 3, 19, 20, 'Remiza', 60 FROM DUAL UNION ALL
SELECT 16, 3, 11, 13, 'Victorie', 90 FROM DUAL UNION ALL
SELECT 17, 4, 12, 14, 'Înfrângere', 45 FROM DUAL UNION ALL
SELECT 18, 4, 15, 17, 'Remiza', 60 FROM DUAL UNION ALL
SELECT 19, 5, 18, 20, 'Victorie', 30 FROM DUAL UNION ALL
SELECT 20, 5, 19, 16, 'Remiza', 45 FROM DUAL;

 
-- Inserarea de date în tabelul "TURNEE"
INSERT INTO TURNEE (id_turneu, nume, data_inceput, data_sfarsit, locatie)
SELECT 1, 'Turneu de Iarn?', DATE '2023-12-01', DATE '2023-12-15', 'Londra' FROM DUAL UNION ALL
SELECT 2, 'Turneu de Prim?var?', DATE '2024-03-15', DATE '2024-03-30', 'Paris' FROM DUAL UNION ALL
SELECT 3, 'Turneu de Var?', DATE '2024-06-01', DATE '2024-06-10', 'Berlin' FROM DUAL UNION ALL
SELECT 4, 'Turneu de Toamn?', DATE '2024-09-01', DATE '2024-09-15', 'Moscova' FROM DUAL UNION ALL
SELECT 5, 'Turneu Final', DATE '2024-12-01', DATE '2024-12-15', 'New York' FROM DUAL UNION ALL
SELECT 6, 'Turneu 1', DATE '2025-02-01', DATE '2025-02-15', 'Bucuresti' FROM DUAL UNION ALL
SELECT 7, 'Turneu 2', DATE '2025-04-15', DATE '2025-04-30', 'Madrid' FROM DUAL UNION ALL
SELECT 8, 'Turneu 3', DATE '2025-07-01', DATE '2025-07-10', 'Viena' FROM DUAL UNION ALL
SELECT 9, 'Turneu 4', DATE '2025-10-01', DATE '2025-10-15', 'Budapesta' FROM DUAL UNION ALL
SELECT 10, 'Turneu 5', DATE '2025-12-01', DATE '2025-12-15', 'Roma' FROM DUAL UNION ALL
SELECT 11, 'Turneu 6', DATE '2026-02-01', DATE '2026-02-15', 'Varsovia' FROM DUAL UNION ALL
SELECT 12, 'Turneu 7', DATE '2026-04-15', DATE '2026-04-30', 'Atena' FROM DUAL UNION ALL
SELECT 13, 'Turneu 8', DATE '2026-07-01', DATE '2026-07-10', 'Praga' FROM DUAL UNION ALL
SELECT 14, 'Turneu 9', DATE '2026-10-01', DATE '2026-10-15', 'Amsterdam' FROM DUAL UNION ALL
SELECT 15, 'Turneu 10', DATE '2026-12-01', DATE '2026-12-15', 'Stockholm' FROM DUAL;
 
-- Inserarea de date în tabelul "CLASAMENTE"
INSERT INTO CLASAMENTE (id_clasament, id_turneu, id_jucator, punctaj, pozitie)
SELECT 1, 1, 1, 8, 1 FROM DUAL UNION ALL
SELECT 2, 1, 2, 7, 2 FROM DUAL UNION ALL
SELECT 3, 1, 3, 6, 3 FROM DUAL UNION ALL
SELECT 4, 2, 4, 10, 1 FROM DUAL UNION ALL
SELECT 5, 2, 5, 8, 2 FROM DUAL UNION ALL
SELECT 6, 2, 6, 6, 3 FROM DUAL UNION ALL
SELECT 7, 3, 7, 9, 1 FROM DUAL UNION ALL
SELECT 8, 3, 8, 8, 2 FROM DUAL UNION ALL
SELECT 9, 3, 9, 7, 3 FROM DUAL UNION ALL
SELECT 10, 4, 10, 10, 1 FROM DUAL UNION ALL
SELECT 11, 4, 11, 7, 2 FROM DUAL UNION ALL
SELECT 12, 4, 12, 6, 3 FROM DUAL UNION ALL
SELECT 13, 5, 13, 9, 1 FROM DUAL UNION ALL
SELECT 14, 5, 14, 8, 2 FROM DUAL UNION ALL
SELECT 15, 5, 15, 7, 3 FROM DUAL UNION ALL
SELECT 16, 1, 16, 10, 1 FROM DUAL UNION ALL
SELECT 17, 1, 17, 8, 2 FROM DUAL UNION ALL
SELECT 18, 1, 18, 7, 3 FROM DUAL UNION ALL
SELECT 19, 2, 19, 9, 1 FROM DUAL UNION ALL
SELECT 20, 2, 20, 8, 2 FROM DUAL;
 
-- Inserarea de date în tabelul "PREMII"
INSERT INTO PREMII (id_premiu, valoare, descriere_premiu)
SELECT 1, 1000, 'Locul 1' FROM DUAL UNION ALL
SELECT 2, 750, 'Locul 2' FROM DUAL UNION ALL
SELECT 3, 500, 'Locul 3' FROM DUAL UNION ALL
SELECT 4, 300, 'Locul 4' FROM DUAL UNION ALL
SELECT 5, 200, 'Locul 5' FROM DUAL;
 
-- Inserarea de date în tabelul "INSCRIERI"
INSERT INTO INSCRIERI (id_inscriere, id_turneu, id_jucator, stare, data_inscriere)
SELECT 1, 1, 1, 'Acceptat', TO_DATE('2023-11-20', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 2, 1, 2, 'Acceptat', TO_DATE('2023-11-25', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 3, 2, 3, 'Acceptat', TO_DATE('2024-02-15', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 4, 2, 4, 'Acceptat', TO_DATE('2024-02-20', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 5, 3, 5, 'Acceptat', TO_DATE('2024-05-01', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 6, 3, 6, 'Acceptat', TO_DATE('2024-05-05', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 7, 4, 7, 'Acceptat', TO_DATE('2024-08-10', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 8, 4, 8, 'Acceptat', TO_DATE('2024-08-15', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 9, 5, 9, 'Acceptat', TO_DATE('2024-11-01', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 10, 5, 10, 'Acceptat', TO_DATE('2024-11-05', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 11, 1, 11, 'Acceptat', TO_DATE('2023-11-18', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 12, 1, 12, 'Acceptat', TO_DATE('2023-11-22', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 13, 2, 13, 'Acceptat', TO_DATE('2024-02-10', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 14, 2, 14, 'Acceptat', TO_DATE('2024-02-15', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 15, 3, 15, 'Acceptat', TO_DATE('2024-05-01', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 16, 3, 16, 'Acceptat', TO_DATE('2024-05-05', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 17, 4, 17, 'Acceptat', TO_DATE('2024-08-10', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 18, 4, 18, 'Acceptat', TO_DATE('2024-08-15', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 19, 5, 19, 'Acceptat', TO_DATE('2024-11-01', 'YYYY-MM-DD') FROM DUAL UNION ALL
SELECT 20, 5, 20, 'Acceptat', TO_DATE('2024-11-05', 'YYYY-MM-DD') FROM DUAL;
 
-- Inserarea de date în tabelul "ECHIPE"
INSERT INTO ECHIPE (id_echipa, nume, id_jucator1, id_jucator2)
SELECT 1, 'Echipa 1', 1, 2 FROM DUAL UNION ALL
SELECT 2, 'Echipa 2', 3, 4 FROM DUAL UNION ALL
SELECT 3, 'Echipa 3', 5, 6 FROM DUAL UNION ALL
SELECT 4, 'Echipa 4', 7, 8 FROM DUAL UNION ALL
SELECT 5, 'Echipa 5', 9, 10 FROM DUAL UNION ALL
SELECT 6, 'Echipa 6', 11, 12 FROM DUAL UNION ALL
SELECT 7, 'Echipa 7', 13, 14 FROM DUAL UNION ALL
SELECT 8, 'Echipa 8', 15, 16 FROM DUAL UNION ALL
SELECT 9, 'Echipa 9', 17, 18 FROM DUAL UNION ALL
SELECT 10, 'Echipa 10', 19, 20 FROM DUAL;
  
-- Inserarea de date în tabelul "JUCATORI_TURNEE"
INSERT INTO JUCATORI_TURNEE (id_jucator, id_turneu, scor)
SELECT 1, 1, 8 FROM DUAL UNION ALL
SELECT 2, 1, 7 FROM DUAL UNION ALL
SELECT 3, 2, 6 FROM DUAL UNION ALL
SELECT 4, 2, 10 FROM DUAL UNION ALL
SELECT 5, 3, 8 FROM DUAL UNION ALL
SELECT 6, 3, 6 FROM DUAL UNION ALL
SELECT 7, 4, 9 FROM DUAL UNION ALL
SELECT 8, 4, 8 FROM DUAL UNION ALL
SELECT 9, 5, 7 FROM DUAL UNION ALL
SELECT 10, 5, 10 FROM DUAL UNION ALL
SELECT 11, 1, 7 FROM DUAL UNION ALL
SELECT 12, 1, 6 FROM DUAL UNION ALL
SELECT 13, 2, 9 FROM DUAL UNION ALL
SELECT 14, 2, 8 FROM DUAL UNION ALL
SELECT 15, 3, 7 FROM DUAL UNION ALL
SELECT 16, 3, 10 FROM DUAL UNION ALL
SELECT 17, 4, 8 FROM DUAL UNION ALL
SELECT 18, 4, 7 FROM DUAL UNION ALL
SELECT 19, 5, 10 FROM DUAL UNION ALL
SELECT 20, 5, 9 FROM DUAL;
  
-- Inserarea de date în tabelul "JUCATORI_PREMII"
INSERT INTO JUCATORI_PREMII (id_jucator, id_premiu)
SELECT 1, 1 FROM DUAL UNION ALL
SELECT 2, 2 FROM DUAL UNION ALL
SELECT 3, 3 FROM DUAL UNION ALL
SELECT 4, 4 FROM DUAL UNION ALL
SELECT 5, 5 FROM DUAL UNION ALL
SELECT 6, 1 FROM DUAL UNION ALL
SELECT 7, 2 FROM DUAL UNION ALL
SELECT 8, 3 FROM DUAL UNION ALL
SELECT 9, 4 FROM DUAL UNION ALL
SELECT 10, 5 FROM DUAL UNION ALL
SELECT 11, 1 FROM DUAL UNION ALL
SELECT 12, 2 FROM DUAL UNION ALL
SELECT 13, 3 FROM DUAL UNION ALL
SELECT 14, 4 FROM DUAL UNION ALL
SELECT 15, 5 FROM DUAL UNION ALL
SELECT 16, 1 FROM DUAL UNION ALL
SELECT 17, 2 FROM DUAL UNION ALL
SELECT 18, 3 FROM DUAL UNION ALL
SELECT 19, 4 FROM DUAL UNION ALL
SELECT 20, 5 FROM DUAL;
  
INSERT INTO TURNEE_ECHIPE (id_turneu_echipa, id_turneu, id_echipa)
SELECT 1, 1, 1 FROM DUAL UNION ALL
SELECT 2, 1, 2 FROM DUAL UNION ALL
SELECT 3, 2, 3 FROM DUAL UNION ALL
SELECT 4, 2, 4 FROM DUAL UNION ALL
SELECT 5, 3, 5 FROM DUAL UNION ALL
SELECT 6, 3, 6 FROM DUAL UNION ALL
SELECT 7, 4, 7 FROM DUAL UNION ALL
SELECT 8, 4, 8 FROM DUAL UNION ALL
SELECT 9, 5, 9 FROM DUAL UNION ALL
SELECT 10, 5, 10 FROM DUAL;
 
6.
Prin Utilizarea Tabloului Indexat:

Acesta va extrage și afișa informații despre jucătorii de șah și scorurile obținute de aceștia în diferite partide.
Pentru fiecare înregistrare din colecție, va afișa numele jucătorului, țara de origine a jucătorului și scorul obținut într-o anumită partidă.
Prin Utilizarea Tabloului Îmbricat:

Acesta va genera și afișa o listă a celor mai recente 10 turnee de șah, ordonate descrescător după data de început.
Pentru fiecare turneu din lista de top 10, va afișa numele turneului și locația unde acesta a avut loc.
Prin Utilizarea unui Vector:

Acesta va crea și afișa o listă ordonată alfabetic a țărilor de origine ale jucătorilor.
Fiecare țară va fi afișată o singură dată în listă, indiferent de numărul de jucători proveniți din acea țară.
Aceste afișări oferă o imagine de ansamblu asupra activității jucătorilor în concursurile de șah, turneele recente și diversitatea geografică a participanților. Subprogramul utilizează colecții diferite pentru a organiza și prezenta datele în moduri variate, demonstrând capacitatea PL/SQL de a manipula și prezenta seturi complexe de date.
CREATE OR REPLACE PROCEDURE RaportConcursSah
IS
    -- Record pentru tabloul indexat
    TYPE t_jucator_rec IS RECORD (
        NumeJucator JUCATORI.nume%TYPE,
        TaraOrigine JUCATORI.tara_origine%TYPE,
        Scor JUCATORI_TURNEE.scor%TYPE
    );

    -- Tablou indexat
    TYPE t_tablou_indexat IS TABLE OF t_jucator_rec INDEX BY PLS_INTEGER;
    t_indexat t_tablou_indexat;

    -- Tablou îmbricat
    TYPE t_tablou_imbricat IS TABLE OF TURNEE%ROWTYPE;
    t_imbricat t_tablou_imbricat := t_tablou_imbricat();

    -- vector
    TYPE t_vector_tari_type IS VARRAY(100) OF JUCATORI.tara_origine%TYPE;
    
    -- Declararea unei variabile de tipul vectorului definit
    t_vector_tari t_vector_tari_type := t_vector_tari_type();


BEGIN
    -- Popularea tabloului indexat cu jucători și scoruri
    FOR rec IN (SELECT j.nume, j.tara_origine, jt.scor FROM JUCATORI j JOIN JUCATORI_TURNEE jt ON j.id_jucator = jt.id_jucator) LOOP
        t_indexat(t_indexat.COUNT + 1).NumeJucator := rec.nume;
        t_indexat(t_indexat.COUNT).TaraOrigine := rec.tara_origine;
        t_indexat(t_indexat.COUNT).Scor := rec.scor;
    END LOOP;

    -- Afișarea rezultatelor tabloului indexat
    FOR i IN t_indexat.FIRST..t_indexat.LAST LOOP
        DBMS_OUTPUT.PUT_LINE(t_indexat(i).NumeJucator || ' din ' || t_indexat(i).TaraOrigine || ' - Scor: ' || t_indexat(i).Scor);
    END LOOP;
    DBMS_OUTPUT.NEW_LINE;

    -- Popularea tabloului îmbricat cu top 10 turnee după numărul de participanți
    FOR rec IN (SELECT * FROM TURNEE ORDER BY data_inceput DESC) LOOP
        t_imbricat.EXTEND;
        t_imbricat(t_imbricat.COUNT) := rec;
        EXIT WHEN t_imbricat.COUNT = 10;
    END LOOP;

    -- Afișarea rezultatelor tabloului îmbricat
    FOR i IN t_imbricat.FIRST..t_imbricat.LAST LOOP
        DBMS_OUTPUT.PUT_LINE(t_imbricat(i).nume || ' - Locatie: ' || t_imbricat(i).locatie);
    END LOOP;
    DBMS_OUTPUT.NEW_LINE;

    -- Popularea vectorului cu țările de origine ale jucătorilor, ordonate alfabetic
    FOR rec IN (SELECT DISTINCT tara_origine FROM JUCATORI ORDER BY tara_origine) LOOP
        IF t_vector_tari.COUNT < t_vector_tari.LIMIT THEN
            t_vector_tari.EXTEND;
            t_vector_tari(t_vector_tari.COUNT) := rec.tara_origine;
        END IF;
    END LOOP;

    -- Afișarea țărilor din vector
    FOR i IN 1..t_vector_tari.COUNT LOOP
        DBMS_OUTPUT.PUT_LINE('Tara: ' || t_vector_tari(i));
    END LOOP;

EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('A aparut o eroare: ' || SQLERRM);
END RaportConcursSah;
/

-- Apelarea subprogramului
BEGIN
    RaportConcursSah;
END;
/
 
7.
create or replace procedure ex7_subprogram_stocat_independent is 
    cursor b is select id_turneu, nume
                from turnee;
    cursor a (param turnee.id_turneu%type) is
            select j.nume, j.tara_origine
            from jucatori j,jucatori_turnee jt
            where jt.id_turneu = param
            and jt.id_jucator=j.id_jucator;

    v_id_turneu turnee.id_turneu%type;
    v_nume_turneu turnee.nume%type;

begin
    open b;
    loop
        fetch b into v_id_turneu, v_nume_turneu;
        exit when b%notfound;

        dbms_output.put_line('-----------------------------------------------');
        dbms_output.put_line('Turneul '||  '   '|| v_nume_turneu);
        dbms_output.put_line('-----------------------------------------------');

        for i in a(v_id_turneu) loop
            dbms_output.put_line(i.nume   || i.tara_origine);
        end loop;
    end loop;
end ex7_subprogram_stocat_independent;
/

begin
    ex7_subprogram_stocat_independent;
end;
/
 
8. Formulați în limbaj natural o problemă pe care să o rezolvați folosind un subprogram stocat independent de tip funcție care să utilizeze într-o singură comandă SQL 3 dintre tabelele definite. Definiți minim 2 excepții proprii. Apelați subprogramul astfel încât să evidențiați toate cazurile definite și tratate
Definiți un subprogram prin care să obțineți rezultatul partidei unui jucator intr-un turneu ael căror id sunt specificate.
create or replace function rezultat_partida_in_turneu
    (v_jucator_id jucatori.id_jucator%TYPE, v_turneu_id turnee.id_turneu%TYPE)
return VARCHAR is
    rezultat partide.rezultat_final%type;
begin
    select p.rezultat_final into rezultat 
    from partide p, jucatori j, turnee t
    where j.id_jucator = v_jucator_id
    and t.id_turneu = v_turneu_id
    and (p.id_jucator_1 = j.id_jucator )
    and p.id_turneu = t.id_turneu;
    return rezultat;
    EXCEPTION
        WHEN NO_DATA_FOUND THEN
            RAISE_APPLICATION_ERROR(-20000, 'Jucatorul nu a participat la acest turneu!');
        WHEN OTHERS THEN
            RAISE_APPLICATION_ERROR(-20001,'Alta eroare!');
end rezultat_partida_in_turneu;
/


BEGIN
    DBMS_OUTPUT.PUT_LINE('Jucatorul a obtinut '|| rezultat_partida_in_turneu('1','4'));
END;
/
 
 



9. Formulați în limbaj natural o problemă pe care să o rezolvați folosind un subprogram stocat independent de tip procedură care să utilizeze într-o singură comandă SQL 5 dintre tabelele definite. Tratați toate excepțiile care pot apărea, incluzând excepțiile NO_DATA_FOUND și TOO_MANY_ROWS. Apelați subprogramul astfel încât să evidențiați toate cazurile tratate.
Definiți un subprogram independent de tip procedură prin care să obțineți premiul obtinut de un jucator intr-un turneu ,fiind specificate numele jucatorului si id-ul turneului.

CREATE OR REPLACE PROCEDURE obtine_premiul_jucator (
    v_nume_jucator IN jucatori.nume%TYPE,
    v_nume_turneu IN turnee.nume%TYPE,
    v_premiu OUT premii.descriere_premiu%TYPE
) IS
BEGIN
SELECT p.descriere_premiu INTO v_premiu
    FROM jucatori j
    JOIN jucatori_turnee jt ON j.id_jucator = jt.id_jucator
    JOIN turnee t ON jt.id_turneu = t.id_turneu
    JOIN jucatori_premii jp ON j.id_jucator = jp.id_jucator
    JOIN premii p ON jp.id_premiu = p.id_premiu
    WHERE j.nume = v_nume_jucator AND t.nume = v_nume_turneu;    
EXCEPTION
    WHEN TOO_MANY_ROWS THEN
        RAISE_APPLICATION_ERROR(-20001,'Exista mai multi jucatori cu numele dat');
    WHEN NO_DATA_FOUND THEN
        v_premiu := NULL;
        RAISE_APPLICATION_ERROR(-20000,'Nu exista date pentru jucatorul sau turneul specificat.');
    WHEN OTHERS THEN
        RAISE_APPLICATION_ERROR(-20002,'Alta eroare!');
END obtine_premiul_jucator;
/

DECLARE
    v_premiu_obtinut premii.descriere_premiu%TYPE;
BEGIN
    obtine_premiul_jucator('John Doe','Turneu de Iarna',v_premiu_obtinut); 
    DBMS_OUTPUT.PUT_LINE('Premiul este: ' || v_premiu_obtinut);
END;
/


 

 



 
 
10.
CREATE OR REPLACE TRIGGER trigger1
    BEFORE INSERT OR UPDATE OR DELETE ON turnee
BEGIN
    IF (TO_CHAR(SYSDATE,'D') = 1)
    OR (TO_CHAR(SYSDATE,'HH24') NOT BETWEEN 8 AND 10)
    THEN
        RAISE_APPLICATION_ERROR(-20001,'tabelul nu poate fi actualizat');
    END IF;
END;
/
 
11.
CREATE OR REPLACE TRIGGER trig2
 BEFORE UPDATE OF durata ON partide
 FOR EACH ROW
BEGIN
  IF (:NEW.durata < :OLD.durata) THEN
    RAISE_APPLICATION_ERROR(-20002,'turneul nu poate incepe mai devreme');
  END IF;
END;
/
 
12.
CREATE TABLE erori ( 
  moment       DATE, 
  utilizator   VARCHAR2(30), 
  nume_baza    VARCHAR2(50), 
  stiva_erori  VARCHAR2(2000) ); 
/ 
CREATE OR REPLACE TRIGGER logerori 
  AFTER SERVERERROR ON DATABASE 
BEGIN 
  INSERT INTO erori 
  VALUES (SYSDATE, SYS.LOGIN_USER, SYS.DATABASE_NAME, 
          DBMS_UTILITY.FORMAT_ERROR_STACK); 
END logerori; 
/
CREATE TABLE erori ( 
  moment       DATE, 
  utilizator   VARCHAR2(30), 
  nume_baza    VARCHAR2(50), 
  stiva_erori  VARCHAR2(2000) ); 
/ 
CREATE OR REPLACE TRIGGER logerori 
  AFTER SERVERERROR ON DATABASE 
BEGIN 
  INSERT INTO erori 
  VALUES (SYSDATE, SYS.LOGIN_USER, SYS.DATABASE_NAME, 
          DBMS_UTILITY.FORMAT_ERROR_STACK); 
END logerori; 
/
CREATE OR REPLACE TRIGGER trig3
AFTER ALTER ON SCHEMA
BEGIN
    dbms_output.put_line('Un tabel a fost modificat: ' || SYS.DICTIONARY_OBJ_NAME);
END;
/

ALTER TABLE partide 
    RENAME COLUMN rezultat_final TO rezultat;
 
