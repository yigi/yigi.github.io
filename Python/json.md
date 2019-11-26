dump fonksiyonu çıktıyı illaki bir dosya içine aktarır. Yani size al bu senin istediğin JSON çıktısı demez. Bunu diyen dumps fonksiyonudur. dumps fonksiyonu str tipinde bir değer döndürürken dump fonksiyonu hiçbir değer döndürmez.

Bu iki fonksiyon da dump ve dumps gibi birbirine çok benziyor. Hatta farkları bile neredeyse aynı. load fonksiyonu sadece dosyadaki JSON verilerini Python verisine çevirirken loads fonksiyonu veriyi parametre olarak alıyor. dump ve dumps’da olduğu gibi parametreleri tamamen aynı.



```python
print(json.dumps({"Ozellikler":{"Hız":150,"Ses":"10db"}},indent=4))
```

```python
{
    "Ozellikler": {
        "Hiz": 150,
        "Ses": "10db"
    }
}
```


__________________________________________________________________


```python
{
  "states": [
    {
      "name": "Alabama",
      "abbreviation": "AL",
      "area_codes": ["205", "251", "256", "334", "938"]
    },
    {
      "name": "Alaska",
      "abbreviation": "AK",
      "area_codes": ["907"]
    },
    {
      "name": "Arizona",
      "abbreviation": "AZ",
      "area_codes": ["480", "520", "602", "623", "928"]
    },
    ...
    ...
    ...
```

```python
import json

with open('states.json') as f:
  data = json.load(f)

for state in data['states']:
  del state['area_codes']

with open('new_states.json', 'w') as f:
  json.dump(data, f, indent=2)
```
