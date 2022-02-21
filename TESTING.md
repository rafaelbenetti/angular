# Testing
 - Unit Tests
 - Integration Tests
 - Regression Tests
 - Stress Tests

## Unit Tests
- It focuses on the smallest unit of software design.

## Integration Tests
- Its focuses on the groups of components that makes one feature or product. 

## Regression Tests
- This type of testing makes sure that the whole component works properly even after adding components to the complete program. 

## Stress Tests
- In this, we give unfavorable conditions to the system and check how they perform in those conditions. 

# Angular Testing
 - Isolated Tests
 - Shallow Tests
 - Integration Tests

## Isolated Tests
- No rendering
- Same as any other JS object test
- Mock all dependencies
- Test a (pipe, component class, service)

```js
import { EmployeeItemComponent } from './employee-item.component';

describe('EmployeeItemComponent (isolated)', () => {
  const component = new EmployeeItemComponent();

  it('should EMIT delete for an employee', () => {
    spyOn(component.delete, 'emit');
    component.onDelete();
    expect(component.delete.emit).toHaveBeenCalled();
  });
});
```

## Shallow Tests
- +Isolated Test
- Render template
- Without children

```js
it('should show all employee properties', () => {
  const el = fixture.nativeElement;

  const name = el.querySelector('.name').innerHTML;
  expect(name).toContain(employee.name);
});
```

## Integration Tests
- Render children
- Only mock browser capabilities
- Check correctness

```js
it('should make a DELETE request on TODOS', () => {
  const details = el.query(By.directive(TodoItemComponent));
  const button = details.nativeElement.querySelector('button');
  button.dispatchEvent(new Event('click'));

  const requestDefault = httpTestingController.expectOne(url);
  requestDefault.flush(items);

  expect(requestDefault.request.method).toBe('GET');

  // Expect one delete from UserDetailsComponent
  const request = httpTestingController.expectOne(`${url}/${items[0]._id}`);
  request.flush({});

  expect(request.request.method).toBe('DELETE');
  httpTestingController.verify();
});
```

### Types of test coverage
- Test coverage is defined as a metric in Software Testing that measures the amount of testing performed by a set of test. 

- In simple terms, it is a technique to ensure that your tests are testing your code or how much of your code you exercised by running the test.

- [Pros] Validates the quality of your tests
- [Pros] It can help to determine the paths in your application that were not tested
Prevent Defect leakage
- [Pros] Defect prevention at an early stage of the project lifecycle

- [Cons] Most of the tasks in the test coverage manual as there are no tools to automate. Therefore, it takes lots of effort to analyze the requirements and create test cases.

## Code Coverage
- Code coverage metrics can help the team monitor their automated tests.

## Test Coverage
- Test coverage means overall test-plan.
- Test coverage is given details about the level to which the written coding of an application has been tested.