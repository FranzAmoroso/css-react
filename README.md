# React + CSS

##### Struttura del progetto

    |-- src/
    |   |-- components/
    |        |-- navbar.jsx
    |        |-- navbar.css
    |   |-- app.jsx
    |   |-- app.css
    |   |-- index.css
    |   |-- main.jsx

## Regole CSS

Nella struttura del progetto, il file `navbar.jsx` contiene la definizione del componente `Navbar`. All'interno di questo componente, se inseriamo un tag `<nav>`, possiamo applicare stili a tale elemento dal file `navbar.css`. La flessibilità di questa struttura consente di utilizzare le regole di stile definite in `navbar.css` anche in altri file CSS all'interno della directory src. In questo modo, le regole di stile non sono limitate al componente nav e possono essere condivise e applicate a diversi componenti all'interno del progetto.

Tuttavia, per limitare le regole CSS al solo componente e migliorare l'isolamento delle stili, possiamo utilizzare diversi metodi:

- Styled Components
- Style Inline
- ClassName o ID
- Stilizzazione Condizionale

#### Style Inline

Il componente `NavBar` utilizza un approccio di stile inline per il tag, limitando le regole CSS al solo componente. In particolare, le regole di stile sono definite mediante un oggetto JavaScript, il quale contiene le specifiche CSS necessarie per personalizzare l'aspetto dell'immagine.

    function NavBar(){
    const img = "vite";
    const imgStyle = {
        height : "200px",
        borderRadius : "30px"
    }
    return (
        <>
        <img style={imgStyle} src={`/${img}.svg`} alt="" />
        </>
        )

    }

le regole di stile definite in `imgStyle` vengono applicate direttamente all'elemento `<img>` tramite l'attributo style. Questo approccio consente di limitare l'ambito delle regole CSS al solo componente NavBar, garantendo un'implementazione più chiara e gestibile.

#### Styled Compontens

Per limitare le regole CSS al solo componente e migliorare l'isolamento delle stili, possiamo utilizzare la libreria `"Styled Components"`.
Con Styled Components, possiamo creare componenti stile direttamente nei file JavaScript o JSX. Questo ci consente di mantenere le regole di stile strettamente associate al componente corrispondente.

    import React from 'react';
    import styled from 'styled-components';

    // Definizione di un componente Styled per il Navbar
    const StyledNavbar = styled.nav`
    /* Regole di stile specifiche per il Navbar */
    background-color: #333;
    color: white;
    padding: 10px;
    `;

    const Navbar = () => {
    return (
        <StyledNavbar>
        {/* Contenuto del componente Navbar */}
        </StyledNavbar>
    );
    }

    export default Navbar;

In questo modo, le regole di stile sono strettamente legate al componente Navbar, garantendo un migliore isolamento delle stili. Puoi adottare lo stesso approccio per altri componenti all'interno del progetto, migliorando così la gestione delle stili nell'ecosistema React.

#### ClassName

In React, l'attributo `className` viene utilizzato per assegnare classi CSS a elementi HTML generati dai componenti React. Questo attributo funziona in modo simile all'attributo class in HTML, ma viene chiamato `className` in React per evitare conflitti con la parola chiave JavaScript class.

###### File CSS

    .immagine-arrotondata { border: 1px solid darkcyan; border-radius: 30px; }
    .grandezza-immagine { height: 200px; width: 200px; }

###### File jsx

    function NavBar() {
        const img = "vite";
        const grandezzaImg = 'grandezza-immagine';

        return (
            <>
                {/* 1. Applicazione dinamica di entrambe le classi */}
                <img className={`immagine-arrotondata ${grandezzaImg}`} src={`/${img}.svg`} alt="" />

                {/* 2. Applicazione dinamica di "grandezza-immagine" */}
                <img className={grandezzaImg} src={`/${img}.svg`} alt="" />

                {/* 3. Applicazione diretta di "immagine-arrotondata" */}
                <img className="immagine-arrotondata" src={`/${img}.svg`} alt="" />
            </>
        );
    }

Il file CSS contiene due classi, `"immagine-arrotondata"` e `"grandezza-immagine"`, con rispettive regole di stile. Nel file JSX, la funzione NavBar utilizza la variabile `grandezzaImg` per aggiungere dinamicamente la classe `"grandezza-immagine"` al tag `<img>`. La classe `"immagine-arrotondata"` nella proprietà className del tag `<img>` viene semplicemente aggiunta direttamente.

#### Stilizzazione Condizionale

La funzione `NavBar` rappresenta un componente React che applica la stilizzazione condizionale a un'immagine in base al valore della variabile x.

    function NavBar() {
        const x = 6;
        const img = "vite";
        const imgStyle = {
        height : x < 10 ? "200px": "500px",
        borderRadius : "30px"
    }

        return (
            <>
                <img className={imgStyle} src={`/${img}.svg`} alt="" />
                <div id="box" className={`rounded ${ x < 10 ? "rotated" : ""}`}></div>
            </>
        );
    }

Utilizzando il linguaggio JSX e le regole di stile dinamiche, nel primo tag `img`, l'altezza dell'immagine viene impostata a `"200px"` se `x` è inferiore a `10`, altrimenti a `"500px"`. La classe "rotated" aggiunge un effetto di rotazione di 45 gradi. Di seguito, nel secondo tag `div` L'applicazione condizionale di questa classe, avviene in base alla condizione `x < 10`. Questo significa che se il valore di `x` è inferiore a `10`, la classe `"rotated"` sarà applicata, aggiungendo l'effetto di rotazione all'elemento `<div>`. In caso contrario, l'effetto di rotazione non verrà applicato.
