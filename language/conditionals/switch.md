# Switch Statements 
**STATUS**: Design Phase 

Switch statements allow you to take an expression and execute code based on certain cases. Each given case can be one or more values, and a default case can be supplied if all other cases fail.

    switch _expression_
        [[
            case [[ _constant_, ... ]] 
                [[ _code_ ]]
            end
        ]]

        [[ _more cases as needed_ ]]

        [[
            default
                [[ _code_ ]]
            end
        ]]
    end

For example,

    var grade = 'A'

    switch a
        case 'A', 'B'
            # nice! 
        end
        case 'C'
            # good job!
        end 
        default
            # uh oh 
        end
    end
