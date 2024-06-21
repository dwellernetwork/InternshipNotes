Make later on a query check if a username already exists within the database.
	something like localhost:1337/api/local/user/id


  

            if (!response.ok) {

                throw new Error('Network response was not ok');

            }

            console.log('Item deleted:', await response.json());

        } else if (item.id) {

            const response = await fetch(`${apiUrl}/${item.id}`, {

                method: 'PUT',

                headers: {

                    Authorization: `Bearer ${jwtToken}`,

                    'Content-Type': 'application/json',

                },

                body: JSON.stringify({

                    data: {

                        user_id: userId,

                        product: item.product_id,

                        quantity: item.quantity,

                        priceSum: item.priceSum

                    }

                }),

            });

  

            if (!response.ok) {

                throw new Error('Network response was not ok');

            }

            console.log('Item updated:', await response.json());

        } else {

            const response = await fetch(apiUrl, {

                method: 'POST',

                headers: {

                    Authorization: `Bearer ${jwtToken}`,

                    'Content-Type': 'application/json',

                },

                body: JSON.stringify({

                    data: {

                        user_id: userId,

                        product: item.product_id,

                        quantity: item.quantity,

                        priceSum: item.priceSum

                    }

                }),

            });

  

            if (!response.ok) {

                throw new Error('Network response was not ok');

            }

            const createdItem = await response.json();

            if (!createdItem.data || !createdItem.data.id) {

                throw new Error('Created item data is invalid');

            }

            item.id = createdItem.data.id;

            console.log('Item created:', createdItem);

        }

    } catch (error) {

        console.error('An error occurred:', error.message);

    }

};