# Petfolio
### Passport for Your Pet

#### Your pet’s medical history on the blockchain so you can access it anywhere.

<hr>


This was a difficult project for us to build in 72 hours. We did the best we can to demonstrate a proof of concept, and meet the minimum qualification of deploying a blockchain application from our local development environment with multiple docker containers to a live server.

The potential for this project is much bigger than the demo we are able to technically implement in this short time. 


#### Please refer to our landing page: https://womeninblockchain2018.github.io/petfolio_lp/

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

# Blockchain Model on Hyperledger Composer:

The basic MVP demo consists of 2 participants, 2 assets, and 2 transactions. 

In the first transaction (Appointment), a new health Record is added to the Pet asset on the ledger. The vet will have permission to make this transaction. In the second transaction, two Owners transfer ownership of a Pet, changing the relationship on all owners and asset involved.

### Excerpt from our Model File:  org.petfolio.cto

```

namespace org.petfolio

asset Pet identified by id {
  o String id
  o String name
  --> Record[] records 
  --> Vet vet
  --> Owner owner
}

transaction Appointment {
  --> Record record
  --> Pet pet
}

transaction Adoption {
  --> Owner newOwner
  --> Pet pet
}

```

### Our Logic Functions:  logic.js

```

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

/**
 * Track the adoption of a pet from one owner to another
 * @param {org.petfolio.Adoption} adoption - the adoption to be processed
 * @transaction
 */

function Adoption(adoption) {

    // set the new owner of the commodity
    adoption.pet.owner = adoption.newOwner;
    return getAssetRegistry('org.petfolio.Pet')
        .then(function(assetRegistry) {

            // persist the state of the commodity
            return assetRegistry.update(adoption.pet);
        });
}

```

Many many thanks to Waleed El Syed in Basel, Switzerland, our wonderful mentor and advisor, who we so lucky to find at the last minute on https://chat.hyperledger.org/ and who agreed to host our Docker containers on his server.

Also many thanks to Colleen and Keit, our conductors at [Women in Blockchain 2018] (https://www.startupbus.com/women-in-blockchain), for bringing us all together.
