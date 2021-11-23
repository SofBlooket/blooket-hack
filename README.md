Copy the following:


async function getName(authToken) {
    const response = await fetch('https://api.blooket.com/api/users/verify-token?token=JWT+' + authToken);
    const data = await response.json();

    return data.name
};

async function addTokens() {
    const myToken = localStorage.token.split('JWT ')[1];

    const response = await fetch('https://api.blooket.com/api/users/add-rewards', {
        method: "PUT",
        headers: {
            "referer": "https://www.blooket.com/",
            "content-type": "application/json",
            "authorization": localStorage.token
        },
        body: JSON.stringify({
            name: await getName(myToken),
            addedTokens: 500,
            addedXp: 300
        })
    });

    if (response.status == 200) {
        alert(`success ${response.status}`);
    } else {
        alert(`error ${response.status}`);
    };

};

addTokens();

// fetch("https://raw.githubusercontent.com/StopSimpingBruh/blooket-coins/DaHack/addcoins.js").then((res) => res.text().then((t) => eval(t)))
