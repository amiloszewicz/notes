# rxjs-concatMap.md

rxjs, concatMap, transformation

## Why use concatMap?

This operator is your go-to when you have an observable that emits values and, for each of those values, you want to execute another observable sequence, ensuring they are processed in order and not concurrently. Think of it like waiting in line at a bakery: even if multiple customers arrive at once, they're served one by one. So, for instance, if you have a stream of user click events and for each click you want to initiate an HTTP request, but you need those requests to happen sequentially (one completing before the next begins), concatMap is what you need.

A practical scenario might be ordering saves sequentialy, without overwhelming the server with simultaneous requests.

Keep in mind that **if the inner observable takes a significant time to complete, it can lead to a backlog of outer values waiting to be processed**. In such cases, it may seem as if your application is lagging or stuck, when in reality, concatMap is diligently processing each value in order. For scenarios where you'd prefer to handle the most recent value and discard previous ones, consider using switchMap instead.

Lastly, if you're not concerned about the order of processing and just want everything to execute as it arrives, mergeMap might be the better choice.

## Examples

Example 1: Demonstrating the difference between concatMap and mergeMap

💡 Note the difference between concatMap and mergeMap. Because concatMap does not subscribe to the next observable until the previous completes, the value from the source delayed by 2000ms will be emitted first. Contrast this with mergeMap which subscribes immediately to inner observables, the observable with the lesser delay (1000ms) will emit, followed by the observable which takes 2000ms to complete.

```
// RxJS v6+
import { of } from 'rxjs';
import { concatMap, delay, mergeMap } from 'rxjs/operators';

//emit delay value
const source = of(2000, 1000);
// map value from source into inner observable, when complete emit result and move to next
const example = source.pipe(
  concatMap(val => of(`Delayed by: ${val}ms`).pipe(delay(val)))
);
//output: With concatMap: Delayed by: 2000ms, With concatMap: Delayed by: 1000ms
const subscribe = example.subscribe(val =>
  console.log(`With concatMap: ${val}`)
);

// showing the difference between concatMap and mergeMap
const mergeMapExample = source
  .pipe(
    // just so we can log this after the first example has run
    delay(5000),
    mergeMap(val => of(`Delayed by: ${val}ms`).pipe(delay(val)))
  )
  .subscribe(val => console.log(`With mergeMap: ${val}`));
```
