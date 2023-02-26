module.exports = async function (context, myBlob) {
    context.log("JavaScript blob trigger function processed blob \n Blob:");
    context.log("********Azure Function Started********");
    var result =true;
    try{
        context.log(myBlob.toString());
        JSON.parse(myBlob.toString().trim().replace('\n', ' '));
    }catch(exception){
        context.log(exception);
        result =false;
    }
    if(result){
        context.bindings.stagingFolder = myBlob.toString();
        context.log("********File Copied to Staging Folder Successfully********");
    } else{
        
        context.bindings.rejectedFolder = myBlob.toString();
        context.log("********Inavlid JSON File Copied to Rejected Folder Successfully********");
    }

    context.log("*******Azure Function Ended Successfully*******");
    
};