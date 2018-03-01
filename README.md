# parse-referenced-objects
parse objects with references properties
# Usage

```js

const res = parse({
        a: 1,
        b: { __$ref: 'a' }
    });
    assert(res.b === res.a);
});

    const res = parse({
        a: 1,
        b: { __$ref: 'c' },
        c: { __$ref: 'a' }
    });
    assert(res.b === res.a);
    assert(res.c === res.a);
});

    const res = parse({
        a: {},
        b: { __$ref: 'c' },
        c: { __$ref: 'a' }
    });
    assert(res.b === res.a);
    assert(res.c === res.a);
});

    const res = parse({
        a: {},
        b: { __$ref: 'reference.to.other.not.exists' }
    });
    assert(res.b === undefined);
});

const res = parse({
    a: {},
    b: {
        bb: {
            __$ref: 'c'
        }
    },
    c: {
        cc: {
            __$ref: 'a'
        }
    }
});
assert(res.b.bb.cc === res.a);
assert(res.c.cc === res.a);
});

const res = parse({
    a: {},
    b: {
        bb: {
            __$ref: 'c'
        }
    },
    c: {
        cc: {
            __$refHere: 'here'
        },
        here: 'hereIAm'
    }
});
assert(res.b.bb.cc === 'hereIAm');
assert(res.c.cc === 'hereIAm');

```


# api

The reference "__$ref" and "__$refHere" are protected to be used like reference inside of object. The path must from parent object or parent direct.


The keys can be changed with REF_KEY and REF_HERE_KEY environment vars.