# `tsx watch` + `concurrently` + `Windows` issue repro

### Reproducing the issue

1. Run `npm install` to install dependencies.
2. Uncomment 1 line out of the first 4 lines in `src/index.ts` and leave the other 3 commented.
3. Run `npm run noIssue1`, then `npm run noIssue2`, then `npm run noIssue3`. You should see **Everything is fine!** in the console.
4. Run `npm run issue` and `tsx watch` will not run, and you will not see **Everything is fine!**.

### Explanation

1. `noIssue1` runs because `tsx watch` is running without `concurrently`.
2. `noIssue2` runs because we removed `watch` out of the `tsx` script.
3. `noIssue3` runs due to a [workaround](https://github.com/vercel/turbo/issues/7834#issuecomment-2033172950) found by the [turbo](https://github.com/vercel/turbo) team.

### Notes

1. `tsx watch` hangs on `Windows` even without using `concurrently` as can be seen on that [previously linked issue](https://github.com/vercel/turbo/issues/7834), which provides more evidence that this issue is not a [concurrenlty](https://www.npmjs.com/package/concurrently) or [turbo](https://github.com/vercel/turbo) issue but rather a [tsx](https://www.npmjs.com/package/tsx) one.
2. The workaround proposed by the turbo team and used on the `noIssue3` script cannot be considered a real solution because `npm` scripts are used on different platforms but `< NUL` is a windows thing.
