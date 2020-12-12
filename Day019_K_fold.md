## 作業目標：運用scikit-learn API 實現K-fold分割資料

---

### 讀入資料


```python
import pandas as pd
dataset = pd.read_csv(r'Social_Network_Ads.csv')
```


```python
dataset
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>User ID</th>
      <th>Gender</th>
      <th>Age</th>
      <th>EstimatedSalary</th>
      <th>Purchased</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15624510</td>
      <td>Male</td>
      <td>19.0</td>
      <td>19000.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15810944</td>
      <td>Male</td>
      <td>35.0</td>
      <td>20000.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15668575</td>
      <td>Female</td>
      <td>26.0</td>
      <td>43000.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15603246</td>
      <td>Female</td>
      <td>27.0</td>
      <td>57000.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>15804002</td>
      <td>Male</td>
      <td>19.0</td>
      <td>76000.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>395</th>
      <td>15691863</td>
      <td>Female</td>
      <td>46.0</td>
      <td>41000.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>396</th>
      <td>15706071</td>
      <td>Male</td>
      <td>51.0</td>
      <td>23000.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>397</th>
      <td>15654296</td>
      <td>Female</td>
      <td>50.0</td>
      <td>20000.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>398</th>
      <td>15755018</td>
      <td>Male</td>
      <td>36.0</td>
      <td>33000.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>399</th>
      <td>15594041</td>
      <td>Female</td>
      <td>49.0</td>
      <td>36000.0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>400 rows × 5 columns</p>
</div>



### 取出訓練特徵與標註


```python
X = dataset[['User ID', 'Gender', 'Age', 'EstimatedSalary']].values
Y = dataset['Purchased'].values
```

---


```python
import numpy as np
from sklearn.model_selection import KFold
```

### 將訓練資料按照順序切割成10等分


```python

kf = KFold(n_splits=5)
kf.get_n_splits(X)

print(kf)

```

    KFold(n_splits=5, random_state=None, shuffle=False)


### 將訓練資料隨機切割成10等分


```python
kf = KFold(n_splits=10)
kf.get_n_splits(X)

print(kf)
```

    KFold(n_splits=10, random_state=None, shuffle=False)


---

### 取出 切割資料對應位置


```python
train_split = kf.split(X)
next(train_split)
```




    (array([ 40,  41,  42,  43,  44,  45,  46,  47,  48,  49,  50,  51,  52,
             53,  54,  55,  56,  57,  58,  59,  60,  61,  62,  63,  64,  65,
             66,  67,  68,  69,  70,  71,  72,  73,  74,  75,  76,  77,  78,
             79,  80,  81,  82,  83,  84,  85,  86,  87,  88,  89,  90,  91,
             92,  93,  94,  95,  96,  97,  98,  99, 100, 101, 102, 103, 104,
            105, 106, 107, 108, 109, 110, 111, 112, 113, 114, 115, 116, 117,
            118, 119, 120, 121, 122, 123, 124, 125, 126, 127, 128, 129, 130,
            131, 132, 133, 134, 135, 136, 137, 138, 139, 140, 141, 142, 143,
            144, 145, 146, 147, 148, 149, 150, 151, 152, 153, 154, 155, 156,
            157, 158, 159, 160, 161, 162, 163, 164, 165, 166, 167, 168, 169,
            170, 171, 172, 173, 174, 175, 176, 177, 178, 179, 180, 181, 182,
            183, 184, 185, 186, 187, 188, 189, 190, 191, 192, 193, 194, 195,
            196, 197, 198, 199, 200, 201, 202, 203, 204, 205, 206, 207, 208,
            209, 210, 211, 212, 213, 214, 215, 216, 217, 218, 219, 220, 221,
            222, 223, 224, 225, 226, 227, 228, 229, 230, 231, 232, 233, 234,
            235, 236, 237, 238, 239, 240, 241, 242, 243, 244, 245, 246, 247,
            248, 249, 250, 251, 252, 253, 254, 255, 256, 257, 258, 259, 260,
            261, 262, 263, 264, 265, 266, 267, 268, 269, 270, 271, 272, 273,
            274, 275, 276, 277, 278, 279, 280, 281, 282, 283, 284, 285, 286,
            287, 288, 289, 290, 291, 292, 293, 294, 295, 296, 297, 298, 299,
            300, 301, 302, 303, 304, 305, 306, 307, 308, 309, 310, 311, 312,
            313, 314, 315, 316, 317, 318, 319, 320, 321, 322, 323, 324, 325,
            326, 327, 328, 329, 330, 331, 332, 333, 334, 335, 336, 337, 338,
            339, 340, 341, 342, 343, 344, 345, 346, 347, 348, 349, 350, 351,
            352, 353, 354, 355, 356, 357, 358, 359, 360, 361, 362, 363, 364,
            365, 366, 367, 368, 369, 370, 371, 372, 373, 374, 375, 376, 377,
            378, 379, 380, 381, 382, 383, 384, 385, 386, 387, 388, 389, 390,
            391, 392, 393, 394, 395, 396, 397, 398, 399]),
     array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
            17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33,
            34, 35, 36, 37, 38, 39]))



### Or


```python
for train_index, test_index in kf.split(X):
    print("TRAIN:", train_index, "TEST:", test_index)
```

    TRAIN: [ 40  41  42  43  44  45  46  47  48  49  50  51  52  53  54  55  56  57
      58  59  60  61  62  63  64  65  66  67  68  69  70  71  72  73  74  75
      76  77  78  79  80  81  82  83  84  85  86  87  88  89  90  91  92  93
      94  95  96  97  98  99 100 101 102 103 104 105 106 107 108 109 110 111
     112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127 128 129
     130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147
     148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 163 164 165
     166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183
     184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 200 201
     202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219
     220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237
     238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255
     256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 271 272 273
     274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 289 290 291
     292 293 294 295 296 297 298 299 300 301 302 303 304 305 306 307 308 309
     310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327
     328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345
     346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363
     364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381
     382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399] TEST: [ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23
     24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39]
    TRAIN: [  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17
      18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35
      36  37  38  39  80  81  82  83  84  85  86  87  88  89  90  91  92  93
      94  95  96  97  98  99 100 101 102 103 104 105 106 107 108 109 110 111
     112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127 128 129
     130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147
     148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 163 164 165
     166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183
     184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 200 201
     202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219
     220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237
     238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255
     256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 271 272 273
     274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 289 290 291
     292 293 294 295 296 297 298 299 300 301 302 303 304 305 306 307 308 309
     310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327
     328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345
     346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363
     364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381
     382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399] TEST: [40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63
     64 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79]
    TRAIN: [  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17
      18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35
      36  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53
      54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71
      72  73  74  75  76  77  78  79 120 121 122 123 124 125 126 127 128 129
     130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147
     148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 163 164 165
     166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183
     184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 200 201
     202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219
     220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237
     238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255
     256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 271 272 273
     274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 289 290 291
     292 293 294 295 296 297 298 299 300 301 302 303 304 305 306 307 308 309
     310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327
     328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345
     346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363
     364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381
     382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399] TEST: [ 80  81  82  83  84  85  86  87  88  89  90  91  92  93  94  95  96  97
      98  99 100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115
     116 117 118 119]
    TRAIN: [  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17
      18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35
      36  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53
      54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71
      72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89
      90  91  92  93  94  95  96  97  98  99 100 101 102 103 104 105 106 107
     108 109 110 111 112 113 114 115 116 117 118 119 160 161 162 163 164 165
     166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183
     184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 200 201
     202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219
     220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237
     238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255
     256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 271 272 273
     274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 289 290 291
     292 293 294 295 296 297 298 299 300 301 302 303 304 305 306 307 308 309
     310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327
     328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345
     346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363
     364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381
     382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399] TEST: [120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137
     138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155
     156 157 158 159]
    TRAIN: [  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17
      18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35
      36  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53
      54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71
      72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89
      90  91  92  93  94  95  96  97  98  99 100 101 102 103 104 105 106 107
     108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125
     126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143
     144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 200 201
     202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219
     220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237
     238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255
     256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 271 272 273
     274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 289 290 291
     292 293 294 295 296 297 298 299 300 301 302 303 304 305 306 307 308 309
     310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327
     328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345
     346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363
     364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381
     382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399] TEST: [160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177
     178 179 180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195
     196 197 198 199]
    TRAIN: [  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17
      18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35
      36  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53
      54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71
      72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89
      90  91  92  93  94  95  96  97  98  99 100 101 102 103 104 105 106 107
     108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125
     126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143
     144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161
     162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179
     180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197
     198 199 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255
     256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 271 272 273
     274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 289 290 291
     292 293 294 295 296 297 298 299 300 301 302 303 304 305 306 307 308 309
     310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327
     328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345
     346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363
     364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381
     382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399] TEST: [200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217
     218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235
     236 237 238 239]
    TRAIN: [  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17
      18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35
      36  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53
      54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71
      72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89
      90  91  92  93  94  95  96  97  98  99 100 101 102 103 104 105 106 107
     108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125
     126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143
     144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161
     162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179
     180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197
     198 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215
     216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233
     234 235 236 237 238 239 280 281 282 283 284 285 286 287 288 289 290 291
     292 293 294 295 296 297 298 299 300 301 302 303 304 305 306 307 308 309
     310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327
     328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345
     346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363
     364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381
     382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399] TEST: [240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255 256 257
     258 259 260 261 262 263 264 265 266 267 268 269 270 271 272 273 274 275
     276 277 278 279]
    TRAIN: [  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17
      18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35
      36  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53
      54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71
      72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89
      90  91  92  93  94  95  96  97  98  99 100 101 102 103 104 105 106 107
     108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125
     126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143
     144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161
     162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179
     180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197
     198 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215
     216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233
     234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251
     252 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 268 269
     270 271 272 273 274 275 276 277 278 279 320 321 322 323 324 325 326 327
     328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345
     346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363
     364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381
     382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399] TEST: [280 281 282 283 284 285 286 287 288 289 290 291 292 293 294 295 296 297
     298 299 300 301 302 303 304 305 306 307 308 309 310 311 312 313 314 315
     316 317 318 319]
    TRAIN: [  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17
      18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35
      36  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53
      54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71
      72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89
      90  91  92  93  94  95  96  97  98  99 100 101 102 103 104 105 106 107
     108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125
     126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143
     144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161
     162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179
     180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197
     198 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215
     216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233
     234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251
     252 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 268 269
     270 271 272 273 274 275 276 277 278 279 280 281 282 283 284 285 286 287
     288 289 290 291 292 293 294 295 296 297 298 299 300 301 302 303 304 305
     306 307 308 309 310 311 312 313 314 315 316 317 318 319 360 361 362 363
     364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381
     382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399] TEST: [320 321 322 323 324 325 326 327 328 329 330 331 332 333 334 335 336 337
     338 339 340 341 342 343 344 345 346 347 348 349 350 351 352 353 354 355
     356 357 358 359]
    TRAIN: [  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17
      18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35
      36  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53
      54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71
      72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89
      90  91  92  93  94  95  96  97  98  99 100 101 102 103 104 105 106 107
     108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125
     126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143
     144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161
     162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179
     180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197
     198 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215
     216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233
     234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251
     252 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 268 269
     270 271 272 273 274 275 276 277 278 279 280 281 282 283 284 285 286 287
     288 289 290 291 292 293 294 295 296 297 298 299 300 301 302 303 304 305
     306 307 308 309 310 311 312 313 314 315 316 317 318 319 320 321 322 323
     324 325 326 327 328 329 330 331 332 333 334 335 336 337 338 339 340 341
     342 343 344 345 346 347 348 349 350 351 352 353 354 355 356 357 358 359] TEST: [360 361 362 363 364 365 366 367 368 369 370 371 372 373 374 375 376 377
     378 379 380 381 382 383 384 385 386 387 388 389 390 391 392 393 394 395
     396 397 398 399]


### 取出切割資料：trainset / testset 特徵(x_train/x_test)/標註(y_train/y_test)


```python
for train_index, test_index in kf.split(X):
    train_X = X[train_index]
    test_X = X[test_index]
    print()
    print(len(train_X),len(test_X))
    print(train_X[0])
    print(test_X[0])
    
```

    
    360 40
    [15764419 'Female' 27.0 17000.0]
    [15624510 'Male' 19.0 19000.0]
    
    360 40
    [15624510 'Male' 19.0 19000.0]
    [15764419 'Female' 27.0 17000.0]
    
    360 40
    [15624510 'Male' 19.0 19000.0]
    [15595917 'Male' 30.0 80000.0]
    
    360 40
    [15624510 'Male' 19.0 19000.0]
    [15811613 'Female' 36.0 75000.0]
    
    360 40
    [15624510 'Male' 19.0 19000.0]
    [15744279 'Male' 32.0 100000.0]
    
    360 40
    [15624510 'Male' 19.0 19000.0]
    [15628523 'Male' 35.0 39000.0]
    
    360 40
    [15624510 'Male' 19.0 19000.0]
    [15701537 'Male' 42.0 149000.0]
    
    360 40
    [15624510 'Male' 19.0 19000.0]
    [15609669 'Female' 59.0 88000.0]
    
    360 40
    [15624510 'Male' 19.0 19000.0]
    [15774872 'Female' 52.0 138000.0]
    
    360 40
    [15624510 'Male' 19.0 19000.0]
    [15577514 'Male' 43.0 129000.0]



```python

```