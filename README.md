# Updating Objects in State

React uygulamalarında, bileşenlerin durumunu yönetmek önemlidir ve bu durum içinde nesneleri güncellemek sıkça karşılaşılan bir ihtiyaçtır. Bu belgede, React'te durum içindeki nesnelerin nasıl güncelleneceğini ve bu süreçte dikkat edilmesi gereken konuları ele alacağız.

## Nedir?

React'te bir bileşenin durumu (state), bileşenin içinde tutulan verilerin bir temsilidir. Durumu güncellemek, kullanıcı etkileşimleri veya veri değişiklikleri gibi olaylara yanıt olarak bileşenin yeniden render edilmesini sağlar. Nesne tipindeki durumları güncellerken, mevcut nesnenin değiştirilmesi yerine, genellikle bir kopyası oluşturulur ve bu kopya üzerinde değişiklikler yapılır.

## Dikkat Edilmesi Gereken Konular

- **Referans Eşleşmesi**: Durum nesnelerini güncellerken, referans eşleşmesine dikkat etmek önemlidir. React, bir bileşenin render edilip edilmeyeceğini referans eşleşmesiyle belirler. Bu nedenle, durum nesnelerini güncellerken, önceki durum nesnesinin referansını korumak önemlidir.
- **Doğrudan Değişiklik Yapmamak**: Durum nesnelerini güncellerken, doğrudan değişiklik yapmaktan kaçınılmalıdır. React, değişmemiş durum nesnelerini algılamak için referans eşleşmesini kullanır. Bu nedenle, mevcut durum nesnesini doğrudan değiştirmek yerine, bir kopya oluşturmak ve onu güncellemek daha iyidir.
- **setState Kullanımı**: setState fonksiyonunu kullanarak durumu güncellemek, React uygulamalarında önerilen yöntemdir. setState, bileşenin yeniden render edilmesini ve güncellenmiş durumun geçerli olmasını sağlar.

## Pratik Kullanımlar

- **Form Verilerini Güncelleme**: Kullanıcı bir formu doldurduğunda, form verilerini durumda güncellemek önemlidir. Bu şekilde, kullanıcı formu doldurduğunda, form verileri bileşenin durumunda saklanabilir ve gerektiğinde güncellenebilir.
- **Liste Elemanlarını Güncelleme**: Bir liste içindeki öğeleri eklemek, kaldırmak veya güncellemek genellikle durum yönetimi gerektirir. Liste elemanları bir nesne olarak saklandığında, bu elemanları güncellemek için durumu güncellemek gerekir.

## Örnek Kod Parçacığı

```javascript
import React, { useState } from 'react';

function App() {
  const [user, setUser] = useState({ name: '', email: '' });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setUser(prevUser => ({
      ...prevUser,
      [name]: value
    }));
  };

  return (
    <div>
      <input
        type="text"
        name="name"
        value={user.name}
        onChange={handleChange}
        placeholder="Name"
      />
      <input
        type="email"
        name="email"
        value={user.email}
        onChange={handleChange}
        placeholder="Email"
      />
    </div>
  );
}
```
## Immer nedir ve nasıl pratiklik sağlar?

Immer, değişken durumları güncellemeyi kolaylaştıran bir kütüphanedir. Özellikle, JavaScript'te nesne veya dizileri değiştirmek ve bu değişiklikleri izlemek zor olabilir. Immer, bu işlemi basitleştirir ve okunabilirliği artırır.

- Daha okunabilir kod: Immer, karmaşık nesne veya diziler üzerinde yapılacak değişiklikleri daha okunabilir hale getirir. Bu, kodun anlaşılmasını ve bakımını kolaylaştırır.

- Yan etkilerden kaçınma: Orijinal veriyi değiştirmeden güncellemeler yaparak, yan etkilerden kaçınabilirsiniz. Bu, kodunuzun daha güvenli ve öngörülebilir olmasını sağlar.

- İşlevsel programlama prensiplerini destekler: Immer, işlevsel programlama prensiplerini destekler ve değişken durumları değiştirmek için işlevsel bir yaklaşım sunar. Bu da daha temiz ve modüler kod yazmanıza olanak tanır.

- Performans: Immer, güncelleme işlemlerini etkili bir şekilde yönetir ve performans kaybını minimize eder. Bu sayede, büyük veri yapıları üzerinde bile verimli bir şekilde çalışabilirsiniz.

```javascript
export default App;


import { useImmer } from 'use-immer';


export default function Form() {

  const [person, updatePerson] = useImmer({
    name: 'Hamza Ali Doğan',
    artwork: {
      title: 'Mutluluğun Resmi',
      city: 'Denizli',
      image: 'https://i.imgur.com/Sd1AgUOm.jpg',
    }
  });


  function handleNameChange(e) {
    updatePerson(draft => {
      draft.name = e.target.value;
    });
  }

  function handleTitleChange(e) {
    updatePerson(draft => {
      draft.artwork.title = e.target.value;
    });
  }


  function handleCityChange(e) {
    updatePerson(draft => {
      draft.artwork.city = e.target.value;
    });
  }

  function handleImageChange(e) {
    updatePerson(draft => {
      draft.artwork.image = e.target.value;
    });
  }

  return (

    <>
      <label>
        Name:
        <input
          value={person.name}
          onChange={handleNameChange}
        />
      </label>

      <label>
        Title:
        <input
          value={person.artwork.title}
          onChange={handleTitleChange}
        />
      </label>

      <label>
        City:
        <input
          value={person.artwork.city}
          onChange={handleCityChange}
        />
      </label>

      <label>
        Image :
        <input
          value={person.artwork.image}
          onChange={handleImageChange}
        />
      </label>

      <p>
        <i>{person.artwork.title}</i>
        {' by '}
        {person.name}
        <br />
        (located in {person.artwork.city})
      </p>
      <img
        src={person.artwork.image}
        alt={person.artwork.title}
      />

    </>


  );
}
```
