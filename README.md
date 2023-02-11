const https = require('https')

async function makeRpcCall(a, b){
    return new Promise((resolve, reject) =>{
        const expression = `${a}+${b}`
        const options = {
            'method': 'GET',
            'hostname': 'localhost',
            'path': '/api/taskcalc/result/'+encodeURI(expression),
        }
        const req = http.request(options, (res)=>{
            const chunks = [];
            res.on('data', (chunk)=>{
                chunks.push(chunk);
            })
            res.on('end', ()=>{
                const data = Buffer.concat(chunks)
                resolve(data.toString());
            });
            res.on('error', (error)=>{
                reject(error);
            })
        })
        req.end();
    })
}

async function call(){
    try{
    const result = await makeRpcCall(2,5) 
    }catch(err){
        console.error(err)
    }
}
call()


------------------------------