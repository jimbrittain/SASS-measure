# SASS measure function/module

## Contents
* `measure` function
* `zeromeasure` function
* `findmeasure_abs` function
* `findmeasure_rel` function
* `measure_isAbsolute` function
## Usage
```
    measure($val, $measurement:'px', $base:$base-font-size, $final_result_is_number:false)
    measure(1em,px,16px) = 16px;
```
* `$val` - a valid united measurement e.g. 1em, 1px, 0px etc. or a number (which is assumed to px)
* `$measuement` - a valid end measurement e.g. em, px, etc.
* `$base` - the base font size, can be globally defined with $base-font-size variable.
* `$final_result_is_number` - Boolean, defaults to false, use to strip the unit if consistency needed in future calculations
### zeromeasure
```
    zeromeasure($unit)
    zeromeasure('em') = 0em;
    zeromeasure('not a valid unit jim') = 0px;
```
$unit accepts *em, ex, px, in, cm, px, pt, %, vw, vh, rem, ch, mm, vmin, vmax, deg*.
Returns a zero unit of the supplied unit string. If unit is not found returns 0px.
### findmeasure_abs
```
    findmeasure_abs($unit)
    findmeasure_abs('in') = 0.010416666667 //in 96 to 1
    findmeasure('not a valid unit jim') = 1 // and a @warn
```
$unit accepts *px, in, cm, mm, pc, pt*.
Returns a float for converting absolute measure from px to alternate absolute unit.
### findmeasure_rel
```
    findmeasure_rel($unit)
    findmeasure_rel(ex) = 0.53 // e.g. 8.48@16 Arial/Helvetica 
    findmeasure_rel('not a valid unit jim') = 1 // and a @warn
```
$unit accetps *em, ex, %, vw, vh, vmin, vmax, rem, ch*.
Returns a float for converting relative measure from em to alternate relative unit.
### measure_isAbsolute
```
    measure_isAbsolute($unit) = true || false
    measure_isAbsolute(px) = true;
    measure_isAbsolute(em) = false;
    measure_isAbsolute('not a valid unit jim') = false;
```
## Issues
* %, vw, vh, vmin, vmax have issues because of base font size. Need to check to ensure works when $base is set to container dimension rather than a px value.
* $base-font-size isn't a good default declaration, should rewrite as if undefined in case of odd import order
