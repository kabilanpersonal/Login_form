app.get('/getOne2/:Projectname', async (req, res) => {
    try{
        const data = await monmodel1.find({project_name: {$regex: req.params.project_name}});
        // res.status(200).json(true)
        res.json(data);
    }
    catch(error){
        res.status(500).json({message: error.message})
    }
})
