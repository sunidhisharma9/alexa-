def lambda_handler(event, context):
    if event['request']['type'] == "LaunchRequest" :
        return onLaunch(event['request'], event['session'])
    elif event['request']['type'] == "IntentRequest" :
        return onIntent(event['request'], event['session'])
    elif event['request']['type'] == "SessionEndedRequest" :
        return onSessionEnd(event['request'], event['session'])

def onLaunch(launchRequest, session):
    return welcomeuser()

def onIntent(intentRequest, session):
             
    intent = intentRequest['intent']
    intentName = intentRequest['intent']['name']
    if intentName == "factIntent":
        return brain_teaser(intent, session)
    elif intentName == "AMAZON.HelpIntent":
        return welcomeuser()
    elif intentName == "AMAZON.CancelIntent" or intentName == "AMAZON.StopIntent":
        return handleSessionEndRequest()
    else:
        raise ValueError("Invalid intent")

def onSessionEnd(sessionEndedRequest, session):
    print("on_session_ended requestId=" + sessionEndedRequest['requestId'] + ", sessionId=" + session['sessionId'])

def welcomeuser():
    sessionAttributes = {}
    cardTitle = " Hello! !"
    speechOutput =  "Hello , Welcome to invention facts " \
                    "You can ask me invention facts by saying tell me a invention fact"
    repromptText =  "You can ask me invention facts by saying tell me a invention fact"
    shouldEndSession = False
    
    return buildResponse(sessionAttributes, buildSpeechletResponse(cardTitle, speechOutput, repromptText, shouldEndSession))

def brain_teaser(intent, session):
    import random
    index = random.randint(0,len(brainteaser)-1)
    cardTitle = " "
    sessionAttributes = {}
    speechOutput = "fact is that " + brainteaser[index] 
    repromptText = "You can ask me invention facts by saying tell me a invention fact"
    shouldEndSession = True                    
    return buildResponse(sessionAttributes, buildSpeechletResponse(cardTitle, speechOutput, repromptText, shouldEndSession))

def handleSessionEndRequest():
    cardTitle = "goodbye "
    speechOutput = "Thank you for using invention facts. " \
                    "Have a great day! "
    shouldEndSession = True
    return buildResponse({}, buildSpeechletResponse(cardTitle, speechOutput, None, shouldEndSession))

def buildSpeechletResponse(title, output, repromptTxt, endSession):
    return {
        'outputSpeech': {
            'type': 'PlainText',
            'text': output
            },
            
        'card': {
            'type': 'Simple',
            'title': title,
            'content': output
            },
            
        'reprompt': {
            'outputSpeech': {
                'type': 'PlainText',
                'text': repromptTxt
                }
            },
        'shouldEndSession': endSession
    }


def buildResponse(sessionAttr , speechlet):
    return {
        'version': '1.0',
        'sessionAttributes': sessionAttr,
        'response': speechlet
    }



brainteaser = [ "Thomas Edison, the inventor of the electric light bulb, motion picture camera and phonograph, was also responsible for the creation of the tattoo pen.",
"Inventor of vaccines and pasteurization,Louis Pasteur was the head of the science program at a French school during the mid 1800's. He once told students that anyone caught smoking would be expelled. Seventy-three of the school's 80 students resigned.",
"The inventor of roller skates, John Joseph Merlin, first demonstrated his creation by careering into a party while playing the violin and crashing into a mirror.",
"Dry cleaning was invented by accident. Someone unintentionally knocked over a kerosene lamp and discovered it could remove stains from their clothes.",
"The inventor of Doritos, Archibald Clark West, had them sprinkled on his grave! His daughter, Jana, stated that plain Doritos (Cool Original) were his favourite.",
"The man who invented the water bed was unable to patent it as the invention had already appeared in science-fiction novels.",
"The inventor of chocolate-chip cookies, Ruth Wakefield, loved chocolate so much that she sold the idea to Nestle in exchange for a lifetime supply of chocolate.",
"Queen Elizabeth I is believed to be the inventor of gingerbread men, as the first documented instance of the sweet treat was at the court of Elizabeth I of England.",
"The same company that invented aspirin, Bayer, also invented heroin as a cold medicine",
"Isaac Newton invented the doggy door .",
"The inventors of Bubble Wrap, Alfred Fielding and Marc Chavannes, were originally trying to make 3d plastic wallpaper, which was a failure.",
" Joseph Bramah, the man who invented the first beer tap also invented the modern toilet.",
"Edison electrocuted an elephant in 1903 to prove Tesla's AC current was dangerous.",
"The inventor of Vaseline used to eat a spoonful of it every day.",
"A 10-Year-Old Accidentally Created in 2012 a New Molecule in Science Class: Tetranitratoxycarbon."
                ]
