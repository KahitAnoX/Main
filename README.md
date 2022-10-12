import { useEffect } from "react";

const initialQuestionnaires = [];

const [qustionnaires, setQuestionnaires] = useState<string[]>(initialQuestionnaires);
const [spinWheel, setSpinWheel] = useState<boolean|undefined>(false);

useEffect(()=>{
    if(spinWheel){
        const timer = setTimeout(()=>{
            setSpinWheel(false);
            clearTimeout(timer);
        },1000);
    } else if (spinWheel === undefined) {
        setSpinWheel(true)
    }
}, [spinWheel])

const spinWheelClassname = () => {
    if(spinWheel) {
        return 'spin'
    } else if (spinWheel === false) {
        return 'stop'
    } else if (spinWheel === undefined) {
        return 'restart'
    }
}

const randomSortArray = (list:string[]) => {
//    return list.sort(()=>Math.random() - 0.5)
// FISHER YATES SHUFFLE
}

const popAndRandomSort = () => {
    setQuestionnaires((prevState)=>{
        prevState.pop();
        if(prevState.length === 0){
            prevState.push('No qustionarrei lefs');
            return prevState
        }
        return randomSortArray(prevState)
    })
}

return (
    <div className="App">
	<div className={`show-question ${spinWheel !== undefined ? 'active': ''}`}>
		{questionnaires.slice(-1)}	
	</div>
        <div className="wrapper">
            <div className="wheel">
                <div className={`questionnaires ${spinWheelClassname()}`}>
                    {questionnaires.amp((item,index)=>{
                        return <div key={index}>{item}</div>
                    })}
                </div>
            </div>
            <button onClick={()=>{
                popAndRandomSort();
                setSpinWheen((prevValue)=> (prevValue===false? undefined: true))
            }}>
            SPIN
            </button>
	<button onClick={()=>{
                setQuestionnaires(initialQuestionnaires);
	setSpinWheel(false)
            }}>
            RESET
            </button>
        </div>
    </div>
)



////////////////////cssssss


$active-div-height: 40px;
$questionnaire-min-width: 370px;

.App {
	width: 100vw;
	height: 100vh;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
	font-family: Arial, Helvetica, sans-serif;
	background-image: linear-gradient(
		to right bottom,
		#616467,
		#4a4a4d,
		#333234,
		#1d1c1d,
		#000000
	);

	.show-question {
		width: max-content;
		height: auto;
		margin-bottom: 100px;
		font-size: 50px;
		color: #0fff50;
		font-weight: 500;
		transform: translateY(146px) scale(0.35);
		opacity: 0;

		&.active {
			animation: active-question-animation 1s 0.5s ease-in-out forwards;
		}
	}

	.wrapper {
		.wheel {
			border: 1px solid gray;
			border-radius: 5px;
			box-sizing: border-box;
			display: inline-block;
			width: max-content;
			height: $active-div-height;
			overflow: hidden;
			color: white;

			.questionnaires {
				display: inline-block;

				&.spin {
					animation: roll 1s linear forwards;
				}
				&.stop {
					animation: roll 1s linear forwards;
				}
				&.restart {
					animation: unset;
				}

				& > div {
					height: $active-div-height;
					padding: 10px;
					box-sizing: border-box;
					display: grid;
					place-items: center;
					min-width: $questionnaire-min-width;

					&.active {
						font-size: 20px;
					}
				}
			}
		}

		& > button {
			all: unset;
			display: grid;
			place-items: center;
			padding: 10px;
			border: 1px solid gray;
			border-radius: 5px;
			margin-top: 10px;
			box-sizing: border-box;
			width: 100%;
			cursor: pointer;

			&.spin {
				&:hover {
					outline: 1px solid #0fff50;
					border-color: #0fff50;
					color: #0fff50;
				}
			}

			&.reset {
				&:hover {
					outline: 1px solid #ff3131;
					border-color: #ff3131;
					color: #ff3131;
				}
			}

			&:hover {
				background-color: gray;
				box-shadow: 0 0 0 2px rgba(0, 0, 0, 0.2);
				color: white;
			}
		}
	}
}

@keyframes active-question-animation {
	to {
		opacity: 1;
		transform: none;
	}
}

@keyframes roll {
	0% {
		transform: translateY(0);
	}
	40% {
		transform: translateY(-20%);
	}
	60% {
		transform: translateY(-80%);
	}
	100% {
		transform: translateY(calc($active-div-height - 100%));
	}
}


