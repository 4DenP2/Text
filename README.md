# Text

            const interCheck = [...checkBoxIdOn];

            if (interCheck.length === 0) {
                interCheck.push(obj.id);
                dispatch(setCheckBoxIdOn(interCheck));
                return;
            }

            const firstIndex = interCheck[interCheck.length - 1];
            const lastIndex = obj.id;

            let found = false;

            sceneCh?.traverse((child: Object3D<Object3DEventMap>): void => {
                if (child.id === firstIndex || child.id === lastIndex) {
                    found = !found;

                    if (found === false) {
                        child.traverse((lastChild: Object3D<Object3DEventMap>): void => {
                            if (!interStructure[lastChild.id].checkBox) {
                                interCheck.push(lastChild.id);
                            }
                        });
                    } else {
                        if (!interStructure[child.id].checkBox) {
                            interCheck.push(child.id);
                        }
                    }
                } else {
                    if (found && !interStructure[child.id].checkBox) {
                        interCheck.push(child.id);
                    }
                }
            });

            dispatch(setCheckBoxIdOn(interCheck));
