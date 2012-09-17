coupon-encode
=============

The purpose of this enconding scheme is generating coupon codes.

It can encode/decode a positive integer in a base 32 scheme where:
  - to make it easy to read over the phone, chars I/L/O are not used
    (avoids confusion with 1/0)
  - char U is not used (to decrease the possibility of f* words)
  - the generated codes are not trivial to guess

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
    