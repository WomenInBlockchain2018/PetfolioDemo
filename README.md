# Petfolio
### Passport for Your Pet

#### Your pet’s medical history on the blockchain so you can access it anywhere.

<hr>


This was a difficult project for us to build in 72 hours. We did the best we can to demonstrate a proof of concept, and meet the minimum qualification of deploying a blockchain application from our local development environment with multiple docker containers to a live server.

The potential for this project is much bigger than the demo we are able to technically implement in this short time. 


#### Please refer to our landing page: https://petfolio.org

<ul>

<li> Our slides and pitchdeck: https://docs.google.com/presentation/d/1VsO_T0plbzr-Ml8Y5ASYU7p-q0gBsdGbuUlKBnBvWPE/edit?usp=sharing </li>

<li> Interactive mockup on InVision: https://projects.invisionapp.com/share/3EHPKZ9JWP7 </li>

<li> Our blockchain demo: https://www.petfolio.co </li>

</ul>

<hr>

# Our Team:

_Presenter & CEO_ - Davia (also a front-end developer)

_Product Manager_ - Shanon 

_UX Designer_ - Kristin 

_Business Development_ - Pam

_Full Stack / Blockchain Dev_ - Kai

<hr>

# Blockchain Model:

The basic demo on Hyperledger Composer consists of 2 participants, 2 assets, and 2 transactions. 

`
asset Pet identified by id {
  o String id
  o String name
  --> Record[] records 
  --> Vet vet
  --> Owner owner
}

/**
 * Track the appointment of a pet with a new health record
 * @param {org.petfolio.Appointment} appointment - the appointment to be processed
 * @transaction
 */
function Appointment(appointment) {

    // set the new owner of the commodity
    appointment.pet.records.push(appointment.record);
    return getAssetRegistry('org.petfolio.Pet')
        .then(function(assetRegistry) {

            // persist the state of the commodity
            return assetRegistry.update(appointment.pet);
        });
}

`
