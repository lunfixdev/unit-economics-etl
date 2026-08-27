# unit-economics-etl

Wewnętrzny pipeline ETL pobierający dane z Allegro REST API co 30 minut w celu obliczania unit economics (jednostkowej rentowności sprzedaży).

## Cel

Pipeline dostarcza dane wejściowe do modelu unit economics: przychód, koszty prowizji Allegro, koszty reklamy oraz koszty fulfillmentu w rozbiciu na zamówienie/ofertę.

## Zakres danych (Allegro API scopes)

- `allegro:api:sale:offers:read` - dane o ofertach, stany magazynowe
- `allegro:api:orders:read` - zamówienia, przychód
- `allegro:api:ads` - wydatki na kampanie reklamowe (Allegro Ads)
- `allegro:api:billing:read` - prowizje i opłaty Allegro
- `allegro:api:fulfillment:read` - dane One Fulfillment (stany magazynowe, awizo)

## Częstotliwość synchronizacji

Pipeline uruchamia się co 30 minut. Synchronizacja jest inkrementalna, oparta na polu `updatedAt`: pobierane są wyłącznie rekordy zmienione od ostatniego uruchomienia.

## Autoryzacja

OAuth2, Device Flow. Access token ważny 12 godzin, refresh token ważny 3 miesiące i odnawiany automatycznie przy każdym uruchomieniu pipeline'u.

## Właściciel

[@dravindel]

## Historia wersji

- `v1.0.0` - pierwsze uruchomienie, pokrycie: orders, offers, ads, billing, fulfillment
