coupon-encode
=============

The purpose of this encoding scheme is generating coupon codes. It
was originally wrote for ClickCupom, a "deal of the day" website in
Brazil.

The standard base32 encoding will generate codes that can be hard to
read over the phone (because of characters like I/l/1 and 
O/0). It also has potential to generate f* words (at least in 
Portuguese) and the sequence is easy to guess.

This special base 32 scheme has the following attributes:

  - to make it easy to read over the phone, chars I/L/O are not used
    (avoids confusion with 1/0)
  - the letter U is not used (to decrease the possibility of f* words)
  - the generated codes are not trivial to guess

By default it will generate 5 digit coupon codes, but can generate
codes with any number of digits.

CouponEncoder()
---------------

Initialize this object with a key made with the characters 'ABCDEFGHJKMNPQRSTWVXYZ0123456789' in random order.

Example:

      >>> c = CouponEncoder('10BEH8G426RADWZVF9JPKX5QMC3YTN7S')
      >>> c.encode(15171013)
      'FS19E'
      >>> c.decode('FS19E')
      15171013
      >>> code, check = c.encode_with_verification(1234)
      ('NH4RZ', '782AV')
      >>> c.is_valid(code, check)
      True
      >>> c.is_valid(code, '782AA')
      False
    